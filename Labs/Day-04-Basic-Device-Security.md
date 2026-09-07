# Day 04 · Protecting Privileged Access and Saving Configuration

[← Lab portfolio](../README.md)

**Environment:** Cisco Packet Tracer, R1 running IOS 15.1

## What I Practiced

This exercise introduced password protection for privileged EXEC mode and the difference between an active configuration and a saved configuration. I inspected how IOS stored an enable password, added an enable secret, returned to privileged mode, and saved the result.

The lab tasks apply to R1 and SW1. The evidence supplied here documents R1; SW1's security configuration is not shown.

## Lab Setup

![Day 4 topology and R1 CLI session](../Photos/Day-04/01-r1-password-configuration.png)

| Device | Model shown | Role |
| --- | --- | --- |
| R1 | Cisco 2911 | Router used for the captured CLI work |
| SW1 | Cisco 2960-24TT | Switch connecting the router and PCs |
| PC1, PC2, PC3 | PC-PT | Endpoints attached to SW1 |

The exercise focuses on device administration. The supplied router configuration has no interface IP addresses, and no traffic tests are included.

## Inspecting Password Storage

I enabled password encryption and inspected the running configuration from configuration mode:

```text
R1(config)#service password-encryption
R1(config)#do sh run
```

Relevant output from my session:

```text
service password-encryption
hostname R1
enable password 7 08026F6028
```

The `7` identifies the stored password format. The lab asks for an initial enable password of `CCNA`; the supplied transcript begins after that initial setup, so it does not show the original password command.

On this lab image, `service password-encryption` changes eligible cleartext password entries to Type 7. Type 7 is reversible obfuscation, not strong protection. The command also does not encrypt network traffic. [Cisco: Protecting Secrets](https://www.cisco.com/c/en/us/about/trust-center/resilient-infrastructure/protecting-secrets.html)

## Adding the Enable Secret

After correcting a spelling error, I entered:

```text
R1(config)#enable secret Cisco
R1(config)#exit
R1#exit
```

I returned to the console and entered privileged EXEC mode:

```text
R1>enable
Password:
Password:
R1#sh run
```

The transcript shows two password prompts followed by `R1#`, confirming that privileged access was eventually obtained. The typed responses are hidden, so the transcript does not establish which value was entered at each prompt.

The running configuration then included both entries:

```text
enable secret 5 $1$mERr$YlCkLMcTYWwkF1Ccndtll.
enable password 7 08026F6028
```

| Question from the exercise | Answer |
| --- | --- |
| Which credential takes precedence? | The enable secret. For this configuration, the lab secret is `Cisco`. |
| What format is the enable password using? | Type 7. |
| What format is the enable secret using? | Type 5 on this IOS image. |
| Does adding a secret remove the password entry? | No; both entries remain visible in this configuration. |

An enable secret takes precedence over an enable password. Type 5 stores an MD5-based hash rather than reversible Type 7 text; it is a legacy format, not a modern password-storage target. These results describe this Packet Tracer image. [Cisco password controls](https://www.cisco.com/c/en/us/td/docs/routers/secure-routers/sec-8100-series/software-config-guide/cisco-8100-series-secure-routers-software-configuration-guide/sec_router_access_pwd_privilege.html), [Cisco credential formats](https://www.cisco.com/c/en/us/about/trust-center/resilient-infrastructure/protecting-secrets.html)

## Two CLI Errors I Corrected

| Attempt | Why IOS rejected it | Working command |
| --- | --- | --- |
| `R1(config)#sh run` | The EXEC command was entered directly in global configuration mode. | `do sh run` |
| `R1(config)#enable sercet Cisco` | `secret` was misspelled. | `enable secret Cisco` |

The first error taught me to check the prompt before entering a command. `R1(config)#` and `R1#` represent different modes. The `do` prefix lets me run an EXEC command while staying in configuration mode.

The second was a syntax mistake. Reading the command again and correcting the keyword resolved it.

## Saving and Checking the Result

I practiced three ways to save the running configuration:

```text
R1#write
Building configuration...
[OK]

R1#write memory
Building configuration...
[OK]

R1#copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
```

These are alternative save commands; running all three is not required. I used them here to practice the available forms.

I then checked the saved configuration:

```text
R1#show startup-config
Using 767 bytes
!
version 15.1
service password-encryption
hostname R1
enable secret 5 $1$mERr$YlCkLMcTYWwkF1Ccndtll.
enable password 7 08026F6028
```

This is an excerpt of the supplied output; unrelated lines are omitted. The saved configuration contains the hostname, password-encryption setting, and both credential entries. That verifies the save operation. A reload test was not recorded.

## Evidence Summary

| Check | Result supported by the session |
| --- | --- |
| Router hostname | `hostname R1` appears in running and startup output. |
| Password representation | Type 7 enable password is visible. |
| Secret representation | Type 5 enable secret is visible. |
| Privileged access | Session returns from `R1>` to `R1#` after password prompts. |
| Persistence | Save commands return `[OK]`; `show startup-config` contains the settings. |
| Switch configuration | SW1 is present in the topology; its CLI verification has not been supplied. |

## What I Will Carry Forward

I learned to use the CLI prompt as a guide to command context, distinguish a password entry from a secret, and verify a save by reading startup configuration. The most useful habit from this exercise is checking the result of a command rather than treating successful entry as the end of the task.

## Saved Material

- [01-r1-password-configuration.png](../Photos/Day-04/01-r1-password-configuration.png) — original topology and R1 screenshot.
- The command excerpts above preserve the relevant results from my pasted CLI session.
- `Labs/day-04-basic-device-security.pkt` can be added when the completed saved file is supplied.
