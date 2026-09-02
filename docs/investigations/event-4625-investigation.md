# Investigation: Windows Event ID 4625 --- Failed Logon

## 1. Investigation Overview

This investigation examines Windows Security Event ID **4625**, which
indicates that a logon attempt failed on the monitored Windows endpoint.

The event was observed through **Wazuh Discover** using the monitored
Windows endpoint (Agent ID `002`).

The investigation focuses on identifying the affected endpoint, the
account involved, the logon type, the reported source address, the
authentication failure, the associated process, the Wazuh detection
rule, and Wazuh's MITRE ATT&CK mapping.

------------------------------------------------------------------------

## 2. Environment

  Component              Value
  ---------------------- ----------------
  SIEM                   Wazuh
  Endpoint               Windows 10
  Wazuh Agent ID         `002`
  Agent Name             `MSEDGEWIN10`
  Event ID               `4625`
  Event Type             Failed Logon
  Investigation Source   Wazuh Discover

> Note: Internal IP addresses shown in screenshots have been sanitized
> before publication in this repository.

------------------------------------------------------------------------

## 3. Investigation Query

The Wazuh Discover investigation was filtered for the monitored endpoint
and Windows Event ID 4625.

``` text
agent.id:002 AND data.win.system.eventID:4625
```

The investigation returned **4 events** during the selected time range.

------------------------------------------------------------------------

## 4. Event Findings

  -----------------------------------------------------------------------------------
  Field                   Observed Value                      Interpretation
  ----------------------- ----------------------------------- -----------------------
  Agent ID                `002`                               Wazuh agent associated
                                                              with the endpoint

  Agent IP                Sanitized in public screenshots     IP address of the
                                                              monitored endpoint

  Agent Name              `MSEDGEWIN10`                       Monitored Windows
                                                              endpoint

  Event ID                `4625`                              Failed logon

  Target Username         `IEUser`                            Account involved in the
                                                              failed authentication

  Target Domain           `MSEDGEWIN10`                       Target Windows
                                                              machine/domain context

  Logon Type              `2`                                 Interactive logon

  Source IP               `127.0.0.1`                         Localhost / loopback
                                                              address

  Workstation Name        `MSEDGEWIN10`                       Workstation associated
                                                              with the event

  Authentication Package  `Negotiate`                         Windows authentication
                                                              package

  Logon Process           `User32`                            Logon process reported
                                                              by Windows

  Process Name            `C:\Windows\System32\svchost.exe`   Process associated with
                                                              the event

  Status                  `0xc000006d`                        Logon failure

  SubStatus               `0xc000006a`                        More specific
                                                              authentication failure
                                                              status

  System Severity         `AUDIT_FAILURE`                     Windows recorded an
                                                              audit failure
  -----------------------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Source IP vs. Agent IP

The `agent.ip` field represents the address associated with the
monitored Windows endpoint communicating with Wazuh.

The `data.win.eventdata.ipAddress` field is the source address recorded
inside the Windows authentication event.

For the examined event:

``` text
agent.ip    = [sanitized Windows endpoint IP]
ipAddress   = 127.0.0.1
```

`127.0.0.1` is the loopback address. Therefore, this particular event
does **not provide evidence of an external Kali Linux source IP**.

This distinction is important because Event ID 4625 alone does not prove
that an external attacker generated the failed authentication.

------------------------------------------------------------------------

## 6. Logon Type Analysis

The event reports:

``` text
Logon Type = 2
```

Logon Type 2 represents an **interactive logon**.

The available event evidence therefore describes the failure as an
interactive authentication event rather than a network logon.

Because the reported source address is `127.0.0.1`, the available
evidence points toward activity associated with the local endpoint
rather than an externally sourced network authentication attempt.

Further correlation is required before attributing the activity to
malicious behavior.

------------------------------------------------------------------------

## 7. Authentication Failure Analysis

The event contains:

``` text
Status    = 0xc000006d
SubStatus = 0xc000006a
```

The Wazuh rule classifies this event as:

``` text
Logon Failure - Unknown user or bad password
```

The substatus is consistent with an authentication attempt involving an
incorrect password.

The evidence therefore supports:

> A failed authentication attempt involving the `IEUser` account was
> recorded on the Windows endpoint.

It does **not** by itself establish that the attempt was performed by an
attacker.

------------------------------------------------------------------------

## 8. Process Information

The event reports:

``` text
Logon Process = User32
Process Name = C:\Windows\System32\svchost.exe
```

The process information is useful for correlation because it identifies
the process context recorded with the authentication event.

Process information should not be interpreted in isolation as proof that
`svchost.exe` itself was malicious. Additional process telemetry,
command-line information, parent/child relationships, and surrounding
events would be required.

------------------------------------------------------------------------

## 9. Wazuh Detection Rule

Wazuh generated the following detection information:

  Field              Value
  ------------------ ----------------------------------------------------
  Rule Description   `Logon Failure - Unknown user or bad password`
  Rule ID            `60122`
  Rule Level         `5`
  Rule Groups        `windows, windows_security, authentication_failed`
  Rule Fired Times   `4`

The rule fired four times during the investigated period.

------------------------------------------------------------------------

## 10. MITRE ATT&CK Mapping

Wazuh reports the following MITRE ATT&CK mapping for this rule:

  Field       Value
  ----------- --------------------------
  MITRE ID    `T1531`
  Tactic      `Impact`
  Technique   `Account Access Removal`

This mapping should be interpreted carefully.

The **Wazuh rule is mapped to T1531**, but the presence of that mapping
does not independently prove that an Account Access Removal technique
was performed during this event.

The underlying Windows event evidence observed here is a failed logon
involving an authentication failure.

Therefore, the MITRE mapping is documented as **Wazuh's rule
classification**, while the investigation conclusion is based on the
underlying event evidence.

------------------------------------------------------------------------

## 11. Event Pattern

The Wazuh Discover search returned four Event ID 4625 records in the
selected period.

Observed timestamps included:

``` text
Aug 28, 2026 @ 09:10:29
Aug 28, 2026 @ 09:10:34
Aug 28, 2026 @ 09:27:45
Aug 28, 2026 @ 09:32:24
```

The events occurred in multiple small groups rather than as a large
continuous burst.

The available evidence shows the same monitored endpoint and the same
general authentication context.

At this stage, the pattern justifies further investigation, but it is
not sufficient to label the activity as a confirmed attack.

------------------------------------------------------------------------

## 12. Initial Assessment

### Observed

-   Windows Event ID 4625 was detected.
-   Four 4625 events were returned by the investigation query.
-   The target account was `IEUser`.
-   The logon type was `2` (interactive).
-   The Windows event reported source address `127.0.0.1`.
-   The authentication package was `Negotiate`.
-   The event was associated with `User32` and `svchost.exe`.
-   Windows recorded `AUDIT_FAILURE`.
-   Wazuh classified the activity as
    `Logon Failure - Unknown user or bad password`.
-   Wazuh mapped the rule to MITRE ATT&CK `T1531`.

### Not established

The available evidence does **not** establish:

-   An external attacker IP
-   A Kali Linux source for these specific events
-   Successful compromise of the Windows endpoint
-   Credential theft
-   Account Access Removal activity
-   Malicious execution by `svchost.exe`

------------------------------------------------------------------------

## 13. Investigation Conclusion

The investigated Event ID 4625 records show repeated failed interactive
authentication attempts involving the `IEUser` account on the monitored
Windows endpoint.

The reported source address for the examined event was `127.0.0.1`,
indicating that the event was associated with the local host rather than
providing evidence of an external source.

The Wazuh detection rule identified the activity as an unknown-user or
bad-password logon failure and generated four detections during the
investigated period.

At this stage, the activity should be considered **suspicious
authentication activity requiring correlation**, rather than confirmed
malicious activity.

The next phase of the lab will intentionally generate controlled
security-testing activity from the authorized Kali Linux VM against the
Windows endpoint. Those events will then be compared with the baseline
events documented here.

------------------------------------------------------------------------

## 14. Evidence

The screenshots associated with this investigation are stored in:

``` text
assets/screenshots/
```

Relevant evidence:

-   `04-event-4625-authentication-details.png`
-   `05-event-4625-rule-mitre-mapping.png`

------------------------------------------------------------------------

## 15. Next Investigation Step

The next step is to perform **event correlation** around the four 4625
records.

The investigation will examine:

1.  Events immediately before and after the failed logons
2.  Related successful logons (Event ID 4624)
3.  Account activity
4.  Process activity
5.  Source addresses
6.  Authentication patterns
7.  Whether additional Wazuh alerts were generated around the same
    timestamps

After the baseline investigation is complete, the lab will move to
controlled, authorized attack simulation from Kali Linux so that the
resulting telemetry can be compared against these baseline events.

------------------------------------------------------------------------

## Disclaimer

This investigation was performed in an isolated, authorized home lab
environment for defensive security learning and SOC analysis.

The documented findings are based on the telemetry available in Wazuh at
the time of investigation and should not be interpreted as proof of
malicious activity without additional correlation and validation.
