# Corrections to the first compiled edition

Corrected publication: 15 October 2026. Locations below refer to the original 163-page PDF. Printed page numbers are one less than PDF page numbers after the cover. The cover, attribution, chapter order, and all 44 chapter start pages are preserved. Windows developments after June 2026 are excluded. This log describes applied changes; it is not a claim of peer review or of testing every Windows version.

## F001: original PDF page 13 (printed 12)

Category: version-dependent behavior

Original:

each one hosting a handful of background services under a shared name

Replacement:

each one hosting one or more background services

Reason: Many modern services have their own host process.

Date and scope: Windows 10 1703 (2017); Microsoft service-host refactoring documentation.

Sources: [Service host grouping in Windows 10](https://learn.microsoft.com/en-us/windows/application-management/svchost-service-refactoring)

## F002: original PDF page 14 (printed 13)

Category: version-dependent behavior

Original:

telemetry level is set to at least "Basic," which is the minimum available outside Enterprise editions.

Replacement:

Windows edition: Home/Pro require Basic; Enterprise, Education, and Server also support diagnostic data off.

Reason: Off is not exclusive to Enterprise.

Date and scope: Microsoft article updated 2025-11-07; edition restrictions predate cutoff.

Sources: [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F003: original PDF page 14 (printed 13)

Category: factual error

Original:

one runs in an elevated user session

Replacement:

one runs as Local Service

Reason: WdiServiceHost uses Local Service, not an elevated interactive user.

Date and scope: Windows Server 2016 service guidance; source frozen before July 2026.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server)

## F004: original PDF page 14 (printed 13)

Category: factual error

Original:

All of these services require at least Basic telemetry to run in their normal capacity; a few, like diagsvc 's scripted diagnostics, need the higher "Enhanced" level.

Replacement:

These services have different dependencies; the diagnostic-data level does not govern all of them. "Enhanced" is a legacy level, unavailable on Windows 11 and Server 2022.

Reason: The blanket Basic/Enhanced dependency is incorrect.

Date and scope: Enhanced limited to Windows 10 1809 and earlier, Server 2016/2019; Microsoft documentation updated 2025-11-07.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server); [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F005: original PDF page 15 (printed 14)

Category: factual error

Original:

Two companion executables do the actual work of capturing a crash: WerFault.exe catches ordinary user-mode crashes, saving minidumps to %LocalAppData%\CrashDumps\along with .wer report files listing the modules involved, the exception code, and a hash of the crash's call stack, then uploads what it captures to watson.microsoft.com . WerFaultSecure.exe handles the more sensitive case of elevated processes and kernel bugchecks, pulling from %SystemRoot%\Minidump\ and reporting to watson.telemetry.microsoft.com .

Replacement:

Two companion executables, WerFault.exe and WerFaultSecure.exe, support crash reporting. WerFault.exe handles ordinary user-mode faults; .wer metadata and attachments belong to WER report folders. Separately, opt-in LocalDumps can write user-mode dumps to %LocalAppData%\CrashDumps\. Uploads depend on settings and consent. Kernel bugcheck dumps use a separate mechanism, with locations governed by CrashControl.

Reason: Correct default-dump assumption, separate report metadata from opt-in LocalDumps, remove unconditional uploads, and distinguish kernel dump creation.

Date and scope: Vista SP1 / Server 2008; Microsoft says not enabled by default.

Sources: [Collecting User-Mode Dumps - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps); [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-wer-reports); [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings); [Varieties of Kernel-Mode Dump Files - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/varieties-of-kernel-mode-dump-files)

## F007: original PDF page 16 (printed 15)

Category: factual error

Original:

records what it finds to %SystemRoot% \AppCompat\Programs\Pca.db

Replacement:

records launch data on Windows 11 22H2 in %SystemRoot%\AppCompat\pca\PcaAppLaunchDic.txt

Reason: The documented PCA launch artifact is not Programs\Pca.db.

Date and scope: Original Sygnia research 2023; Windows 11 22H2 artifact (2022).

Sources: [pca-research](https://www.sygnia.co/blog/new-windows-11-pca-artifact/)

## F008: original PDF page 16 (printed 15)

Category: factual error

Original:

The Application Information service ( Appinfo ) logs every UAC elevation request, capturing the process ID, parent process ID, binary path, and user SID involved, which shows up in the Security event log as event ID 4688 if process-creation auditing is turned on.

Replacement:

The Application Information service (Appinfo) handles UAC elevation requests. When process-creation auditing is enabled, Security event ID 4688 records new processes, including their process ID, creator process ID, image path, and account context.

Reason: 4688 is process-creation auditing, not an AppInfo log of every UAC request.

Date and scope: Microsoft event 4688 documentation dated 2022-01-24; event since Vista/Server 2008.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server); [4688(S) A new process has been created. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4688)

## F009: original PDF page 19 (printed 18)

Category: factual error

Original:

%AppData% \Microsoft\Windows\Notifications\wpndatabase.db

Replacement:

%LocalAppData%\Microsoft\Windows\Notifications\wpndatabase.db

Reason: Database is in Local, not Roaming, AppData.

Date and scope: Original Dissect parser pinned 2026-06-10; notification research published January 2022.

Sources: [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F010: original PDF page 22 (printed 21)

Category: factual error

Original:

Netlogon logs domain logon events and secure channel traffic to %SystemRoot%\debug\netlogon.log .

Replacement:

When debug logging is enabled, Netlogon logs authentication and secure-channel activity to %SystemRoot%\debug\netlogon.log.

Reason: Verbose Netlogon logging must not be assumed enabled.

Date and scope: Microsoft KB 109626, including Server 2012 R2 and later; frozen pre-cutoff.

Sources: [Enable debug logging for Netlogon service - Windows Client](https://learn.microsoft.com/en-us/troubleshoot/windows-client/windows-security/enable-debug-logging-netlogon-service)

## F011: original PDF page 22 (printed 21)

Category: factual error

Original:

every process creation, network connection, file operation, registry operation, logon event, and memory event

Replacement:

selected process, network, file, registry, logon, and memory-related events

Reason: MDE collects selected telemetry, not a guaranteed record of every operation.

Date and scope: Microsoft DeviceEvents schema documentation ms.date 2025-03-28, updated 2026-06-26; it describes security-generated events rather than a complete trace of every operation.

Sources: [DeviceEvents table in the advanced hunting schema - Microsoft Defender XDR](https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-deviceevents-table)

## F012: original PDF page 23 (printed 22)

Category: factual error

Original:

of every client that accessed a role like SMB, IIS, Remote Desktop Services, DNS, or DHCP on that server

Replacement:

of client activity reported by roles and products that support UAL on that server

Reason: UAL is not an exhaustive log for every role.

Date and scope: Windows Server 2012 UAL design; Microsoft pre-cutoff documentation.

Sources: [Get Started with User Access Logging](https://learn.microsoft.com/en-us/windows-server/administration/user-access-logging/get-started-with-user-access-logging)

## F013: original PDF page 24 (printed 23)

Category: factual error

Original:

backed by a SQLite store called unistore.dll

Replacement:

backed by an ESE database named store.vol, used by Windows Mail

Reason: unistore.dll is a library, not a SQLite store.

Date and scope: H. Chivers, Navigating the Windows Mail database (2018), DOI 10.1016/j.diin.2018.02.001.

Sources: [Navigating the Windows Mail database](https://eprints.whiterose.ac.uk/133161/1/Navigating_the_Windows_Mail_database_accepted.pdf); [Per-user services](https://learn.microsoft.com/en-us/windows/application-management/per-user-services-in-windows)

## F014: original PDF page 26 (printed 25)

Category: version-dependent behavior

Original:

Since Windows 8, prefetch files use a compressed format called v30

Replacement:

Windows 10 introduced compressed v30 Prefetch files

Reason: Compressed MAM/v30 begins with Windows 10.

Date and scope: Primary specification records Windows 10 compression in June 2015; distinguishes v26 on Windows 8/8.1.

Sources: [prefetch-spec](https://github.com/libyal/libscca/blob/9d7bea874099d1f35c906cd7ca4872fd045fa748/documentation/Windows%20Prefetch%20File%20%28PF%29%20format.asciidoc)

## F015: original PDF page 26 (printed 25)

Category: factual error

Original:

the file opens with a four-byte

Replacement:

the file starts with a version and a four-byte

Reason: Version DWORD precedes SCCA.

Date and scope: Original Prefetch format specification, pinned 2026-06-29.

Sources: [prefetch-spec](https://github.com/libyal/libscca/blob/9d7bea874099d1f35c906cd7ca4872fd045fa748/documentation/Windows%20Prefetch%20File%20%28PF%29%20format.asciidoc)

## F016: original PDF page 27 (printed 26)

Category: factual error

Original:

signature reading SCCA , followed by a version marker, the

Replacement:

signature reading SCCA, reserved bytes, the

Reason: SCCA at 4, reserved DWORD at 8, file size at 12.

Date and scope: Original Prefetch format specification, pinned 2026-06-29.

Sources: [prefetch-spec](https://github.com/libyal/libscca/blob/9d7bea874099d1f35c906cd7ca4872fd045fa748/documentation/Windows%20Prefetch%20File%20%28PF%29%20format.asciidoc)

## F017: original PDF page 27 (printed 26)

Category: outdated information

Original:

Windows keeps at most 128 prefetch files on a workstation

Replacement:

The limit is 128 files on Windows 7, normally 1,024 on Windows 8 and later

Reason: 128 is the older Windows 7 limit.

Date and scope: Original forensic research published 2016 documents 1,024 on Windows 8.

Sources: [Digital Forensics – Prefetch Artifacts](https://countuponsecurity.com/2016/05/16/digital-forensics-prefetch-artifacts/)

## F018: original PDF page 28 (printed 27)

Category: factual error

Original:

a SHA-1 hash of the first 31.5 kilobytes of the file

Replacement:

a SHA-1 hash of up to the first 31,457,280 bytes (30 MiB) of the file

Reason: The stated unit is wrong; smaller files are hashed in full.

Date and scope: NVISO experiments 2022-03-07, updated 2022-03-21, Windows 8/10.

Sources: [Amcache contains SHA-1 Hash – It Depends!](https://blog.nviso.eu/2022/03/07/amcache-contains-sha-1-hash-it-depends/)

## F019: original PDF page 28 (printed 27)

Category: factual error

Original:

The closest thing Amcache has to an execution timestamp is the LastWriteTime of the InventoryApplicationFile key itself, which

Replacement:

The LastWriteTime of an InventoryApplicationFile key records an inventory update, which

Reason: Inventory timing is not an execution timestamp.

Date and scope: ANSSI original Amcache analysis, 2019-01-21.

Sources: [Analyse de l’AmCache](https://cyber.gouv.fr/nous-connaitre/publications/publications-scientifiques/analyse-de-lamcache/)

## F020: original PDF page 29 (printed 28)

Category: factual error

Original:

approximates when that entry was last touched, but the source research is careful to call this a proxy rather than an authoritative execution time.

Replacement:

approximates when that entry was last touched, not when the executable ran.

Reason: Continue the corrected interpretation over the page break.

Date and scope: ANSSI original Amcache analysis, 2019-01-21.

Sources: [Analyse de l’AmCache](https://cyber.gouv.fr/nous-connaitre/publications/publications-scientifiques/analyse-de-lamcache/)

## F021: original PDF page 29 (printed 28)

Category: outdated information

Original:

only for the 128 most recently run programs

Replacement:

within a finite cache, normally up to 1,024 files on Windows 8 and later

Reason: Second occurrence of obsolete retention limit.

Date and scope: Original Windows 8 retention research, 2016.

Sources: [Digital Forensics – Prefetch Artifacts](https://countuponsecurity.com/2016/05/16/digital-forensics-prefetch-artifacts/)

## F022: original PDF page 30 (printed 29)

Category: factual error

Original:

{5C8CF1C7-7257-4F13-B223-970EF5939312}

Replacement:

{D10CA2FE-6FCF-4F6D-848E-B2E99266FA89}

Reason: Original GUID is Application Timeline, not Resource Usage.

Date and scope: Original SRUM format specification pinned 2021-06-05.

Sources: [srum-spec](https://github.com/libyal/esedb-kb/blob/7308a338353a7c416b58207853bedc45289a1b7c/documentation/System%20Resource%20Usage%20Monitor%20%28SRUM%29.asciidoc)

## F023: original PDF page 31 (printed 30)

Category: factual error

Original:

{DA73FB89-2BEA-4DDC-86B8-6E048C6DA477}

Replacement:

{973F5D5C-1D90-4944-BE8E-24B94231A174}

Reason: Original GUID is Energy Estimator, not Network Data Usage.

Date and scope: SRUM specification 2021-06-05; srum-dump configuration 2025-04-19.

Sources: [srum-spec](https://github.com/libyal/esedb-kb/blob/7308a338353a7c416b58207853bedc45289a1b7c/documentation/System%20Resource%20Usage%20Monitor%20%28SRUM%29.asciidoc); [srum-config](https://github.com/MarkBaggett/srum-dump/blob/1d412262a5de3eec2810d18a37d3a769617f003c/configuration_file.md)

## F024: original PDF page 31 (printed 30)

Category: factual error

Original:

SRUM is locked while Windows is running, so live collection needs either a volume shadow copy or the srum service stopped first.

Replacement:

SRUDB.dat is usually locked while Windows runs; live collection can use a shadow copy, raw NTFS access, or a copy after stopping the Diagnostic Policy Service (DPS).

Reason: SRUM is integrated with DPS, not a service named srum; raw NTFS collection is also possible.

Date and scope: Khatri original Windows 8 study, 2015; Cohen live-collection research, 2019-12-31.

Sources: [Yogesh Khatri: Forensic implications of System Resource Usage Monitor (SRUM) data in Windows 8](https://www.sciencedirect.com/science/article/pii/S1742287615000031); [Digging into the System Resource Usage Monitor (SRUM)](https://www.velociraptor-docs.org/blog/2019/2019-12-31_digging-into-the-system-resource-usage-monitor-srum-afbadb1a375/)

## F025: original PDF page 31 (printed 30)

Category: factual error

Original:

Because every timestamp is bucketed to the hour, SRUM alone can't pin down precise execution moments

Replacement:

Many SRUM records combine activity over an hour, so their timestamps alone do not show exactly when a program ran

Reason: Flush interval is not the resolution of every timestamp/field.

Date and scope: Primary SRUM format specification pinned 2021-06-05.

Sources: [srum-spec](https://github.com/libyal/esedb-kb/blob/7308a338353a7c416b58207853bedc45289a1b7c/documentation/System%20Resource%20Usage%20Monitor%20%28SRUM%29.asciidoc); [Digging into the System Resource Usage Monitor (SRUM)](https://www.velociraptor-docs.org/blog/2019/2019-12-31_digging-into-the-system-resource-usage-monitor-srum-afbadb1a375/)

## F026: original PDF page 32 (printed 31)

Category: version-dependent behavior

Original:

with a mirrored key under dam for desktop-visible applications specifically

Replacement:

with related dam keys on supported builds

Reason: DAM is a connected-standby moderator, not a mirror for visible desktop apps.

Date and scope: Windows 8 DAM documentation; BAM research 2020-04-08.

Sources: [Desktop Activity Moderator - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/w8cookbook/desktop-activity-moderator); [BAM internals](https://dfir.ru/2020/04/08/bam-internals/)

## F027: original PDF page 32 (printed 31)

Category: factual error

Original:

every executed binary appears as its own registry value

Replacement:

a recorded binary appears as its own registry value

Reason: BAM does not cover every executable or launch route.

Date and scope: Original BAM reverse engineering 2020-04-08.

Sources: [BAM internals](https://dfir.ru/2020/04/08/bam-internals/)

## F028: original PDF page 33 (printed 32)

Category: factual error

Original:

investigating it in real time isn't possible; it has to be pulled from an offline hive copy, a volume shadow copy, or a memory acquisition.

Replacement:

the key can still be queried live with sufficient permissions; offline hive copies, shadow copies, and memory acquisitions offer other ways to read it.

Reason: A locked hive file does not prevent live registry queries.

Date and scope: Registry APIs since Windows 2000; original BAM research used live state in 2020.

Sources: [BAM internals](https://dfir.ru/2020/04/08/bam-internals/); [RegQueryValueExW function (winreg.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regqueryvalueexw)

## F029: original PDF page 33 (printed 32)

Category: version-dependent behavior

Original:

entries persist across reboots because the hive is flushed to disk on every clean shutdown

Replacement:

entries can survive reboots, but researched Windows 10 builds purge entries older than seven days during boot

Reason: BAM boot-time retention purge is omitted.

Date and scope: Original reverse engineering 2020-04-08, updated 2020-04-09.

Sources: [BAM internals](https://dfir.ru/2020/04/08/bam-internals/)

## F030: original PDF page 34 (printed 33)

Category: factual error

Original:

periodically captures a screenshot of your entire desktop

Replacement:

when the user opts in, periodically captures snapshots of eligible screen content

Reason: Recall is opt-in and excludes filtered/ineligible content.

Date and scope: Microsoft architecture announcement 2024-09-27, updated 2024-10-01.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)

## F031: original PDF page 34 (printed 33)

Category: factual error

Original:

and a Screenshots subfolder holding the actual images as JPEG files, each one DPAPI-encrypted with a key tied to your user account, named roughly after their capture timestamp.

Replacement:

and encrypted image data under ImageStore. Keys are protected by TPM hardware, Windows Hello sign-in, and a VBS enclave, a protected area of memory. Paths and formats vary by build.

Reason: The book combines early-preview artifacts with an inaccurate DPAPI/JPEG model.

Date and scope: Microsoft architecture 2024-09-27; original schema research frozen at 2026-04-08.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/); [recall-schema](https://github.com/xaitax/TotalRecall/blob/1b6f20289b77829ca334c9e35a2435b62b554735/README.md)

## F032: original PDF page 34 (printed 33)

Category: factual error

Original:

A WindowCapture table logs each snapshot's Unix timestamp, the title bar text of the active window at that moment, the process name responsible for it, the process ID, the logon session ID, and a token hash used in decryption. An ImageToken table links each capture to its file on disk and records the image's pixel dimensions. An Activity table is where the semantic indexing happens: each row classifies the capture by activity type (browsing, editing, viewing,

Replacement:

In builds examined by TotalRecall, WindowCapture records timestamps, titles, bounds, and an ImageToken column. WindowCaptureTextIndex indexes window titles and OCR text; related tables link captures to applications, websites, files, and topics. The tables vary by build, and this metadata can describe browsing, editing, viewing,

Reason: ImageToken/Activity/ExtractedText/AppInfo do not match the analyzed schema.

Date and scope: Original Recall schema research at commit dated 2026-04-08, explicitly build-dependent.

Sources: [recall-schema](https://github.com/xaitax/TotalRecall/blob/1b6f20289b77829ca334c9e35a2435b62b554735/README.md)

## F033: original PDF page 35 (printed 34)

Category: factual error

Original:

communicating, and so on) and, critically, stores an ExtractedText field holding whatever OCR pulled off the screen, plus a JSON field of named entities extracted from that text. A companion AppInfo table simply maps application identifiers to friendly names and icon paths.

Replacement:

communicating, and other activities. The structures holding OCR text vary by build. The App table maps application identifiers to names, paths, and icon metadata.

Reason: Continue the corrected schema across the page break.

Date and scope: Original schema research frozen at 2026-04-08.

Sources: [recall-schema](https://github.com/xaitax/TotalRecall/blob/1b6f20289b77829ca334c9e35a2435b62b554735/README.md)

## F034: original PDF page 35 (printed 34)

Category: factual error

Original:

That ExtractedText column

Replacement:

That indexed OCR text

Reason: Remove the nonexistent column reference.

Date and scope: Original schema research frozen at 2026-04-08.

Sources: [recall-schema](https://github.com/xaitax/TotalRecall/blob/1b6f20289b77829ca334c9e35a2435b62b554735/README.md)

## F035: original PDF page 35 (printed 34)

Category: factual error

Original:

The screenshots themselves are DPAPI-encrypted, but DPAPI decryption is derivable from the user's own credentials, specifically their NTLM hash combined with the protection blob stored at %AppData%\Microsoft\Protect\{SID} \ , a mechanism explained in more detail in part twelve.

Replacement:

The released design uses Windows Hello Enhanced Sign-in Security (ESS) and the enclave to protect access to the encrypted snapshots and index. An NTLM hash and ordinary DPAPI master-key files alone do not provide those Recall keys.

Reason: The released key protection is not ordinary user DPAPI derivable from NTLM credentials.

Date and scope: Microsoft redesigned architecture 2024-09-27; management documentation dated 2025-12-10.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/); [Manage Recall for Windows clients](https://learn.microsoft.com/en-us/windows/client-management/manage-recall)

## F036: original PDF page 35 (printed 34)

Category: factual error

Original:

HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsAI\IsEnabled

Replacement:

HKCU\SOFTWARE\Policies\Microsoft\Windows\WindowsAI\DisableAIDataAnalysis=1

Reason: Use the documented Turn off saving snapshots policy.

Date and scope: DisableAIDataAnalysis is identified in Microsoft Recall documentation dated 2025-12-02; its Windows 11 24H2 applicability starts with KB5055627 (April 2025). The current CSP page is used only for this existing policy mapping, not its later additions.

Sources: [WindowsAI Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai); [Manage Recall for Windows clients](https://learn.microsoft.com/en-us/windows/client-management/manage-recall); [Recall overview - Windows apps](https://learn.microsoft.com/en-us/windows/apps/develop/windows-integration/recall/)

## F037: original PDF page 35 (printed 34)

Category: version-dependent behavior

Original:

by default it retains its snapshots for a configurable window, up to about three months or until it hits a storage limit, whichever comes first.

Replacement:

retention depends on configured duration and storage limits; three months is not a universal maximum.

Reason: Microsoft documents options beyond 90 days; sources describe different defaults, so no universal default is selected.

Date and scope: Microsoft management documentation 2025-12-10; original TotalRecall research at immutable 2026-04-08 commit. These describe different defaults; no post-June default is selected.

Sources: [Manage Recall for Windows clients](https://learn.microsoft.com/en-us/windows/client-management/manage-recall); [recall-schema](https://github.com/xaitax/TotalRecall/blob/1b6f20289b77829ca334c9e35a2435b62b554735/README.md)

## F038: original PDF page 35 (printed 34)

Category: factual error

Original:

amounts to close to a complete reconstruction of everything the user did, saw, and typed during the retention window

Replacement:

can reveal sensitive screen content from eligible snapshots kept during that window

Reason: Filtered, paused, unsupported, or unsaved activity is not a complete record.

Date and scope: Microsoft security and privacy architecture 2024-09-27.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)

## F039: original PDF page 37 (printed 36)

Category: factual error

Original:

HFRE\Qrfxgbc\zlevf.rkr decodes straightforwardly to USER\Desktop\myexe.exe

Replacement:

HFRE\Qrfxgbc\zlrkr.rkr decodes straightforwardly to USER\Desktop\myexe.exe

Reason: Original sample decodes to myris.exe; replacement ROT13 checked locally.

Date and scope: Stable ROT13 mapping; UserAssist parser pinned 2021-05-08.

Sources: [userassist-parser](https://github.com/keydet89/RegRipper3.0/blob/bf3a916ad9ccc5214ea15bf833d14acc97c0b3f0/plugins/userassist.pl)

## F040: original PDF page 37 (printed 36)

Category: factual error

Original:

Interestingly, the GUID key names themselves are ROT13'd too, so the encoded form of {CEBFF5CD-...} reads {PRHSS5PQ-...} .

Replacement:

The GUID key names themselves are not ROT13-encoded.

Reason: GUID keys are literal; value names are decoded.

Date and scope: Original RegRipper UserAssist parser 2021-05-08.

Sources: [userassist-parser](https://github.com/keydet89/RegRipper3.0/blob/bf3a916ad9ccc5214ea15bf833d14acc97c0b3f0/plugins/userassist.pl)

## F041: original PDF page 38 (printed 37)

Category: factual error

Original:

thirty-six bytes of largely unused padding

Replacement:

forty-four bytes of intervening data

Reason: Gap from 0x10 to 0x3C is 44 bytes; not all intervening fields are established as padding.

Date and scope: Modern layout parsed before 2021-05-08; offset arithmetic checked.

Sources: [userassist-parser](https://github.com/keydet89/RegRipper3.0/blob/bf3a916ad9ccc5214ea15bf833d14acc97c0b3f0/plugins/userassist.pl); [userassist-rekall](https://github.com/google/rekall/blob/v1.7.1/rekall-core/rekall/plugins/windows/registry/userassist.py)

## F042: original PDF page 38 (printed 37)

Category: version-dependent behavior

Original:

on modern Windows, the counter doesn't start at one. The very first recorded execution shows a run count of five, because Microsoft changed the starting value to avoid a display glitch involving very-low counts, which means a value of five could represent either five real runs or, just as easily, exactly one.

Replacement:

the older 16-byte format used a five-count bias. That adjustment does not apply to modern 72-byte entries, so a modern value of five cannot be read as one run on that basis.

Reason: The bias belongs to the legacy format; the display-glitch explanation is unsupported.

Date and scope: Original parser distinguishes 16-byte and 72-byte entries; commit 2021-05-08.

Sources: [userassist-parser](https://github.com/keydet89/RegRipper3.0/blob/bf3a916ad9ccc5214ea15bf833d14acc97c0b3f0/plugins/userassist.pl); [userassist-rekall](https://github.com/google/rekall/blob/v1.7.1/rekall-core/rekall/plugins/windows/registry/userassist.py)

## F043: original PDF page 38 (printed 37)

Category: factual error

Original:

tamper-resistant timestamp

Replacement:

corroborating timestamp

Reason: Registry metadata is not tamper-resistant evidence.

Date and scope: Documented registry metadata interfaces and editable hive structures predate cutoff.

Sources: [RegQueryValueExW function (winreg.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regqueryvalueexw)

## F044: original PDF page 39 (printed 38)

Category: version-dependent behavior

Original:

records applications launched specifically through the Windows Search box

Replacement:

records recent app activity on Windows 10 1607/1703

Reason: Not a general modern Windows 10/11 or exclusively Search artifact.

Date and scope: Original research 2020-10-23 confirms 1607/1703 and reports uncertainty on 1709.

Sources: [When did RecentApps go?](https://thinkdfir.com/2020/10/23/when-did-recentapps-go/); [recentapps-artifact](https://github.com/Velocidex/velociraptor/blob/e851953bd5bcff06a6e026ae6bb7a2cbd6de1cab/artifacts/definitions/Windows/Forensics/RecentApps.yaml)

## F045: original PDF page 39 (printed 38)

Category: factual error

Original:

An application that shows up here but is absent from UserAssist tells you something specific: it was launched by typing into Search rather than clicking through the shell.

Replacement:

RecentApps without UserAssist does not prove a Search launch. Sources disagree on 1709; later builds generally do not populate this key.

Reason: Absence from an incomplete artifact does not prove a launch route; preserve source disagreement.

Date and scope: 2020-10-23 original experiments versus Velociraptor's broader 1607–1709 range, pinned 2026-05-17.

Sources: [When did RecentApps go?](https://thinkdfir.com/2020/10/23/when-did-recentapps-go/); [recentapps-artifact](https://github.com/Velocidex/velociraptor/blob/e851953bd5bcff06a6e026ae6bb7a2cbd6de1cab/artifacts/definitions/Windows/Forensics/RecentApps.yaml)

## F046: original PDF page 39 (printed 38)

Category: factual error

Original:

tracks Alt+Tab and Task View interaction directly.

Replacement:

tracks taskbar interaction.

Reason: These counters are taskbar interactions.

Date and scope: CrowdStrike original experiments 2020-05-18.

Sources: [How to Employ FeatureUsage for Windows 10 Taskbar Forensics](https://www.crowdstrike.com/en-us/blog/how-to-employ-featureusage-for-windows-10-taskbar-forensics/)

## F047: original PDF page 40 (printed 39)

Category: factual error

Original:

was selected while cycling through Alt+Tab, and its ShowJumpView subkey does the same for Task View (Win+Tab).

Replacement:

was selected through the taskbar, and ShowJumpView counts taskbar jump-list displays, such as a right-click on an app icon.

Reason: ShowJumpView is not Task View.

Date and scope: CrowdStrike original experiments 2020-05-18.

Sources: [How to Employ FeatureUsage for Windows 10 Taskbar Forensics](https://www.crowdstrike.com/en-us/blog/how-to-employ-featureusage-for-windows-10-taskbar-forensics/)

## F048: original PDF page 40 (printed 39)

Category: factual error

Original:

it fires whenever a window is selected in the switcher

Replacement:

it can record a taskbar selection

Reason: Remove the remaining incorrect switcher trigger.

Date and scope: CrowdStrike original experiments 2020-05-18.

Sources: [How to Employ FeatureUsage for Windows 10 Taskbar Forensics](https://www.crowdstrike.com/en-us/blog/how-to-employ-featureusage-for-windows-10-taskbar-forensics/)

## F049: original PDF page 43 (printed 42)

Category: factual error

Original:

Every folder a user has ever opened in Explorer gets a trace here

Replacement:

Folders a user opens in Explorer can leave traces here

Reason: Shellbags are a cache, not a guaranteed exhaustive navigation record.

Date and scope: Original parser/specification frozen before July 2026.

Sources: [shellbags-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/regf/shellbags.py)

## F050: original PDF page 44 (printed 43)

Category: factual error

Original:

a signature value of 0xBEEF ), it also carries full FILETIME-precision creation, modification, and access timestamps

Replacement:

a signature such as 0xBEEF0004), it also carries DOS/FAT-format creation and access timestamps

Reason: Common extension timestamps use DOS/FAT resolution; modification is in base shell item.

Date and scope: Primary shell-item specification pinned 2026-06-23, with older format history.

Sources: [shellitem-spec](https://github.com/libyal/libfwsi/blob/7ffa7a3bdadae5314919599c2c1b3e2bdda18633/documentation/Windows%20Shell%20Item%20format.asciidoc)

## F051: original PDF page 44 (printed 43)

Category: factual error

Original:

even though the precise timestamp for any individual folder comes from the FILETIME fields embedded in that folder's own PIDL node, not from the registry key's metadata.

Replacement:

but timestamps inside the PIDL describe the folder's own file times, not the visit.

Reason: Filesystem metadata is not a precise navigation timestamp.

Date and scope: Original specification and parser pinned before cutoff.

Sources: [shellitem-spec](https://github.com/libyal/libfwsi/blob/7ffa7a3bdadae5314919599c2c1b3e2bdda18633/documentation/Windows%20Shell%20Item%20format.asciidoc); [shellbags-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/regf/shellbags.py)

## F052: original PDF page 45 (printed 44)

Category: factual error

Original:

a program that opens a file by calling the Windows API directly, bypassing Explorer's dialogs entirely, leaves no LNK file behind.

Replacement:

direct file I/O alone does not request a recent-item shortcut, though an application can explicitly call SHAddToRecentDocs.

Reason: Applications may update recent documents without Explorer dialogs.

Date and scope: Microsoft API documentation includes XP/Vista/Windows 7 behavior.

Sources: [SHAddToRecentDocs function (shlobj_core.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/shlobj_core/nf-shlobj_core-shaddtorecentdocs)

## F053: original PDF page 47 (printed 46)

Category: factual error

Original:

record when the shortcut itself was last accessed by the user

Replacement:

reflect filesystem activity, not necessarily a user opening the target

Reason: A shortcut filesystem timestamp is not necessarily a user access event.

Date and scope: Original LNK specification 2023-09-28; Microsoft file-times documentation before cutoff.

Sources: [lnk-spec](https://github.com/libyal/liblnk/blob/2ca55f4a8f853d5d5b9f573649582b23f2481493/documentation/Windows%20Shortcut%20File%20%28LNK%29%20format.asciidoc); [File Times - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/sysinfo/file-times)

## F054: original PDF page 48 (printed 47)

Category: factual error

Original:

9b9cdc69c1c24e2b for Explorer itself, 1bc392b8e104a00e for Notepad, and, notably, 35235b892d6b3422 for mshta.exe and f0275e776c87a65b for powershell.exe , both frequently checked by investigators specifically because those two tools show up so often in attacker tooling.

Replacement:

1b4dd67f29cb1962 for Windows Explorer, 9b9cdc69c1c24e2b for 64-bit Notepad, and 1bc392b8e104a00e for Windows 7 Remote Desktop Connection. Identifiers can vary; resolve unfamiliar hashes against a documented mapping.

Reason: Two labels are demonstrably wrong; alleged mshta/PowerShell hashes cannot be authenticated, so no speculative relabeling.

Date and scope: Original JumpList AppIDs resource pinned 2026-02-03.

Sources: [jumplist-appids](https://github.com/EricZimmerman/JumpList/blob/fde58dd6b1f6082539d7e38f286241c1048ac31c/JumpList/Resources/AppIDs.txt)

## F055: original PDF page 48 (printed 47)

Category: factual error

Original:

a pin-status byte ( 0xFF meaning not pinned, 0x00 meaning pinned)

Replacement:

a 32-bit pin status (0xFFFFFFFF meaning unpinned, nonnegative values indicating a pin position)

Reason: Pin status is a DWORD, not a byte or binary 0/FF choice.

Date and scope: Original JumpList format specification 2015-01-05.

Sources: [jumplist-spec](https://github.com/EricZimmerman/documentation/blob/2bfe536edd3acf062ffa7331e0b39131eddd42d5/Jump%20lists%20format.asciidoc)

## F056: original PDF page 49 (printed 48)

Category: factual error

Original:

but it is not called by direct API-level file access, by command-line tools, or by UWP apps, which use an entirely different WinRT mechanism instead.

Replacement:

but direct file I/O alone does not call it; applications may explicitly request recent-item updates, and packaged apps also have WinRT access-list mechanisms.

Reason: Direct-API applications are not categorically excluded.

Date and scope: Microsoft API documentation predating cutoff.

Sources: [SHAddToRecentDocs function (shlobj_core.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/shlobj_core/nf-shlobj_core-shaddtorecentdocs)

## F057: original PDF page 49 (printed 48)

Category: version-dependent behavior

Original:

How many entries the folder retains is controlled by HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\MaxRecentDocs , defaulting to twenty for what's shown in the Start menu, though the folder on disk typically holds more than that.

Replacement:

HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\MaxRecentDocs controls the legacy Recent Items menu, whose default is ten items; it does not set a universal retention limit for files on disk.

Reason: The documented policy limits the displayed Recent Items menu and gives a default of ten. It is not a universal disk-artifact retention cap.

Date and scope: Microsoft ADMX policy page 2025-03-12; applicability includes Windows 10 2004/20H2 with KB5005101 (2021).

Sources: [ADMX_WindowsExplorer Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-admx-windowsexplorer)

## F058: original PDF page 51 (printed 50)

Category: factual error

Original:

It's also the set that a call to the standard SetFileTime() API can rewrite freely

Replacement:

SetFileTime() can change creation, access, and write times, but not MFT change time

Reason: SetFileTime has three timestamp pointers, not all four MACB values.

Date and scope: Microsoft API supports XP/Server 2003; frozen pre-cutoff source.

Sources: [SetFileTime function (fileapi.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-setfiletime)

## F059: original PDF page 53 (printed 52)

Category: factual error

Original:

Any file downloaded from the internet gets a Zone.Identifier stream attached automatically

Replacement:

Supporting downloaders can attach a Zone.Identifier stream

Reason: MOTW depends on downloader, filesystem, policy, and origin.

Date and scope: Microsoft Attachment Manager documentation predates cutoff.

Sources: [IAttachmentExecute (shobjidl_core.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/shobjidl_core/nn-shobjidl_core-iattachmentexecute)

## F060: original PDF page 54 (printed 53)

Category: factual error

Original:

and again inaccessible through ordinary Win32 calls

Replacement:

and accessible through the Win32 USN-journal control calls

Reason: Documented DeviceIoControl FSCTLs provide access.

Date and scope: Microsoft FSCTL_QUERY_USN_JOURNAL/READ_USN_JOURNAL support XP and later.

Sources: [FSCTL_READ_USN_JOURNAL - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winioctl/ni-winioctl-fsctl_read_usn_journal); [FSCTL_QUERY_USN_JOURNAL - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winioctl/ni-winioctl-fsctl_query_usn_journal)

## F061: original PDF page 59 (printed 58)

Category: outdated information

Original:

across event IDs 1 through 25

Replacement:

including event IDs above 25

Reason: Events 26–29 existed before cutoff.

Date and scope: Microsoft Sysmon documentation frozen 2026-06-19.

Sources: [Sysmon - Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

## F062: original PDF page 59 (printed 58)

Category: factual error

Original:

whenever an unsigned SMB connection gets blocked

Replacement:

when an insecure guest logon is rejected

Reason: 31017 is RejectedInsecureGuestAuth.

Date and scope: Microsoft event table in Windows Server documentation frozen before cutoff.

Sources: [Enable insecure guest logons in SMB2 and SMB3 for Windows client and Windows Server](https://learn.microsoft.com/en-us/windows-server/storage/file-server/enable-insecure-guest-logons-smb2-and-smb3)

## F063: original PDF page 59 (printed 58)

Category: factual error

Original:

device connection and disconnection (event IDs 400 and 410)

Replacement:

device configuration and start (event IDs 400 and 410)

Reason: 400 configured, 410 started; not generic disconnect events.

Date and scope: Microsoft Windows 10 1607 assurance report and original event metadata.

Sources: [pnp-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-Kernel-PnP.xml)

## F064: original PDF page 61 (printed 60)

Category: factual error

Original:

an XML metadata file

Replacement:

a text metadata file containing key=value fields

Reason: Report.wer differs from XML companion metadata.

Date and scope: Microsoft WER report sample from 2017 distinguishes .wer from WERInternalMetadata.xml.

Sources: [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-wer-reports)

## F065: original PDF page 61 (printed 60)

Category: factual error

Original:

which is generated for essentially every application crash

Replacement:

when dump collection is enabled and succeeds

Reason: Dump capture is configurable and may fail.

Date and scope: Microsoft WER documentation since Vista SP1/Server 2008.

Sources: [Collecting User-Mode Dumps - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps); [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings)

## F066: original PDF page 62 (printed 61)

Category: factual error

Original:

The Report.wer XML file is where most of the useful, human-readable detail lives. An OSVersionInformation block records the exact Windows version and build. A ProcessInformation block gives the crashing process's ID, image name, uptime at the moment of the crash, and parent process ID. The most detailed section, ProblemSignatures , opens with an EventType field and then ten numbered parameters whose meaning depends on that type.

Replacement:

The Report.wer text file holds much of the useful, human-readable detail. EventType identifies the report type, while Sig[n].Name and Sig[n].Value pairs label the problem-signature fields. Other fields vary by report type and build; XML companion files may hold more OS and process metadata.

Reason: The passage assigns XML companion structures to Report.wer and invents universal blocks/counts.

Date and scope: Microsoft sample report from 2017 and Windows 8.1 UMDF metadata documentation.

Sources: [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-wer-reports); [Accessing UMDF Metadata in WER Reports - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/wdf/accessing-umdf-metadata-in-wer-reports)

## F067: original PDF page 62 (printed 61)

Category: factual error

Original:

The exception code recorded in the fourth parameter

Replacement:

The named exception-code field

Reason: APPCRASH generally uses Sig[6]; use named fields rather than a universal ordinal.

Date and scope: Original APPCRASH examples predate cutoff.

Sources: [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-WER-reports)

## F068: original PDF page 62 (printed 61)

Category: factual error

Original:

0xC0000409 specifically indicates a stack buffer overrun caught by the

Replacement:

0xC0000409 can also mark a deliberate fast-fail stop, not only a stack overrun caught by the

Reason: Generic fast-fail termination also uses this status.

Date and scope: Microsoft __fastfail native support since Windows 8; pre-cutoff documentation.

Sources: [__fastfail](https://learn.microsoft.com/en-us/cpp/intrinsics/fastfail?view=msvc-170)

## F069: original PDF page 63 (printed 62)

Category: factual error

Original:

compiler's /GS protection, a strong signal of an attempted exploitation.

Replacement:

compiler's /GS protection and does not by itself establish exploitation.

Reason: Continue corrected interpretation across page break.

Date and scope: Microsoft __fastfail documentation predates cutoff.

Sources: [__fastfail](https://learn.microsoft.com/en-us/cpp/intrinsics/fastfail?view=msvc-170)

## F070: original PDF page 63 (printed 62)

Category: factual error

Original:

0xE06D7363 and 0xE0434352 are the internal codes .NET and C++ use to represent their own managed exceptions, recognizable by the ASCII text hidden inside the hex ( msc and CCR respectively).

Replacement:

0xE06D7363 identifies Microsoft C++ exceptions, while 0xE0434352 identifies CLR/.NET exceptions; neither alone establishes an exploitation attempt.

Reason: Languages reversed; native C++ exceptions are not CLR managed exceptions.

Date and scope: Microsoft C++ explanation 2010-07-30; CLR exception documentation predates cutoff.

Sources: [Decoding the parameters of a thrown C++ exception (0xE06D7363) - The Old New Thing](https://devblogs.microsoft.com/oldnewthing/20100730-00/?p=13273); [CLR Exception E0434352](https://learn.microsoft.com/en-us/shows/inside/e0434352)

## F071: original PDF page 63 (printed 62)

Category: factual error

Original:

Every minidump, whether generated for an application or the kernel, follows the same underlying MINIDUMP format.

Replacement:

User-mode minidumps use MINIDUMP; kernel small dumps use a different format.

Reason: Kernel small dumps do not share user-mode MINIDUMP_HEADER format.

Date and scope: Microsoft kernel dump and MINIDUMP_HEADER references frozen before cutoff.

Sources: [MINIDUMP_HEADER (minidumpapiset.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_header); [Varieties of Kernel-Mode Dump Files - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/varieties-of-kernel-mode-dump-files)

## F072: original PDF page 64 (printed 63)

Category: factual error

Original:

DontSendAdditionalData stops heap dumps specifically from being sent to Microsoft

Replacement:

DontSendAdditionalData suppresses additional, second-level report data

Reason: Not specifically a heap-dump toggle.

Date and scope: Microsoft WER settings 2022-05-17.

Sources: [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings)

## F073: original PDF page 64 (printed 63)

Category: factual error

Original:

LoggingDisabled disables local reporting altogether

Replacement:

LoggingDisabled disables WER logging

Reason: Logging is not all reporting or dump capture.

Date and scope: Microsoft WER settings 2022-05-17.

Sources: [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings)

## F074: original PDF page 64 (printed 63)

Category: factual error

Original:

DebugApplications subkey can redirect a crash straight to a debugger instead of WER for a named executable

Replacement:

DebugApplications subkey controls whether users must choose Debug or Continue for a named executable

Reason: This controls a user choice, not a debugger redirection command.

Date and scope: Microsoft WER settings 2022-05-17.

Sources: [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings)

## F075: original PDF page 65 (printed 64)

Category: factual error

Original:

Buried in Windows since Vista

Replacement:

Buried in Windows since Windows 7

Reason: PSR was introduced in Windows 7.

Date and scope: Microsoft Windows 7 article 2011-04-25.

Sources: [Being productive at work with Windows 7](https://blogs.windows.com/windowsexperience/2011/04/25/being-productive-at-work-with-windows-7/)

## F077: original PDF page 67 (printed 66)

Category: version-dependent behavior

Original:

Volatility3's hibernation plugin, or Arsenal Recon's dedicated Hibernation Recon tool, can extract and analyze it directly.

Replacement:

Arsenal Recon's Hibernation Recon can extract supported formats; Volatility 3 requires suitable hibernation-layer or conversion support.

Reason: Standard generally available hibernation-plugin support must not be assumed.

Date and scope: Volatility contributor discussion 2025-10-07/08 describes separate PR/conversion support.

Sources: [Image copy · Issue #1887 · volatilityfoundation/volatility3](https://github.com/volatilityfoundation/volatility3/issues/1887); [hibernation-recon](https://arsenalrecon.com/products/hibernation-recon)

## F078: original PDF page 67 (printed 66)

Category: factual error

Original:

a narrower role specific to Modern Standby

Replacement:

a narrower role in reclaiming memory from suspended packaged apps

Reason: swapfile.sys is not specific to Modern Standby.

Date and scope: Microsoft Windows 8/Server 2012 explanation; official migrated article modified 2019-03-16.

Sources: [Windows 8 / Windows Server 2012: The New Swap File | Microsoft Community Hub](https://techcommunity.microsoft.com/blog/askperf/windows-8--windows-server-2012-the-new-swap-file/375155)

## F079: original PDF page 23 (printed 22)

Category: version-dependent behavior

Original:

storing it all in a database called Windows.edb

Replacement:

using Windows.edb or Windows.db

Reason: Search storage is not universally ESE.

Date and scope: Original parser pinned 2026-06-10 identifies Windows 11 22H2 SQLite.

Sources: [search-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/search.py)

## F080: original PDF page 70 (printed 69)

Category: factual error

Original:

maps file paths and cache entry IDs together and stores hashes of those file paths

Replacement:

maps thumbnail identifiers to cache entries; it is not a complete path-to-image history

Reason: Index does not supply the asserted full path history.

Date and scope: Original thumbnail specification 2024-05-18 and parser 2026-06-10.

Sources: [thumbcache-spec](https://github.com/libyal/libwtcdb/blob/0e7b48a57377203834d1cedc038134fef51f572a/documentation/Windows%20Explorer%20Thumbnail%20Cache%20database%20format.asciidoc); [thumbcache-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/thumbcache.py)

## F081: original PDF page 70 (printed 69)

Category: factual error

Original:

a thumbnail cache entry proves a file existed and was visible in Explorer

Replacement:

a thumbnail can outlive its source, without proving the user viewed it

Reason: Generation is not conclusive evidence of viewing.

Date and scope: Original specification and parser predate cutoff.

Sources: [thumbcache-spec](https://github.com/libyal/libwtcdb/blob/0e7b48a57377203834d1cedc038134fef51f572a/documentation/Windows%20Explorer%20Thumbnail%20Cache%20database%20format.asciidoc); [thumbcache-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/thumbcache.py)

## F082: original PDF page 70 (printed 69)

Category: factual error

Original:

Each entry carries a cache entry hash, a hash of the original file's path, the data size, a modified timestamp, and the actual thumbnail image data itself

Replacement:

Entries hold cache identifiers, sizes, checksums, and image data; finding source paths and times needs other evidence

Reason: The common entry header lacks the stated modified-time field.

Date and scope: Original header specification pinned 2024-05-18.

Sources: [thumbcache-spec](https://github.com/libyal/libwtcdb/blob/0e7b48a57377203834d1cedc038134fef51f572a/documentation/Windows%20Explorer%20Thumbnail%20Cache%20database%20format.asciidoc); [thumbcache-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/thumbcache.py)

## F083: original PDF page 71 (printed 70)

Category: version-dependent behavior

Original:

Windows.edb , built in the ESE database format and maintained

Replacement:

Windows.edb (ESE) or Windows.db (SQLite), and is maintained

Reason: Add covered version difference.

Date and scope: Original parser 2026-06-10 labels Windows 11 22H2 SQLite.

Sources: [search-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/search.py)

## F084: original PDF page 72 (printed 71)

Category: factual error

Original:

Sitting alongside the search index, a smaller and much less documented file called WaitList.dat supports a related but distinct feature: Windows' people-centric search suggestions, the mechanism behind predictive contact and file suggestions that used to surface through Cortana and still partly underpins the modern Search experience. Rather than indexing file content, it maintains a ranked, frequency-weighted record of the people and items a user interacts with most, feeding that ranking back into search suggestions and predictive text. Precisely because it's built to model behavior rather than to index content, its presence and contents are worth treating as a general signal of which contacts and items a user engaged with most heavily over time, even without needing to fully reverse its internal structure the way this book has done for better-documented artifacts elsewhere.

Replacement:

A separate, less documented file called WaitList.dat supports input personalization. Original research on Windows 8.1 found text and metadata from emails, contacts, and documents harvested through the search indexer, including content whose source was no longer available. Its location was %LocalAppData%\Microsoft\InputPersonalization\TextHarvester\. It is not merely a people-frequency ranking: the retained text itself can be forensic evidence. Availability and contents depend on the system's version and personalization settings.

Reason: Wrong purpose and evidence interpretation; preserve original artifact coverage.

Date and scope: Barnaby Skeggs research 2016-11-03, updated 2020-05-12.

Sources: [Touch Screen Lexicon Forensics (TextHarvester / WaitList.dat) - Forensic Focus](https://www.forensicfocus.com/articles/touch-screen-lexicon-forensics-textharvester-waitlist-dat/)

## F085: original PDF page 73 (printed 72)

Category: outdated information

Original:

If the signed-in account is syncing activity, the same data gets pushed to activityfeed.microsoft.com

Replacement:

Older activity-sync configurations sent data to activityfeed.microsoft.com

Reason: MSA uploads stopped in 2021; Windows 11 send-history option deprecated in January 2024.

Date and scope: July 2021 change in original parser; Microsoft KB5034204, 2024-01-23.

Sources: [activity-history](https://support.microsoft.com/en-us/windows/privacy/windows-activity-history-and-your-privacy); [timeline-parser](https://github.com/kacos2000/WindowsTimeline/blob/696293696cc5d6ed6b5c82cb61139883b6a6505b/README.md)

## F086: original PDF page 74 (printed 73)

Category: factual error

Original:

though two values are consistently observed: 11 represents a clipboard copy event and 12 represents a share or send operation.

Replacement:

though the WindowsTimeline research maps 10 to clipboard text and 16 to copy/paste, with 11 and 12 covering Windows system operations.

Reason: Incorrect supposedly consistent type mappings.

Date and scope: Original WindowsTimeline README 2023-02-16; Dissect parser 2026-06-10.

Sources: [timeline-parser](https://github.com/kacos2000/WindowsTimeline/blob/696293696cc5d6ed6b5c82cb61139883b6a6505b/README.md); [activities-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/activitiescache.py)

## F087: original PDF page 75 (printed 74)

Category: factual error

Original:

%LocalAppData%\Microsoft\Phone Link

Replacement:

its Microsoft.YourPhone app package under %LocalAppData%\Packages

Reason: Package data, not the stated Microsoft\Phone Link directory; multiple databases vary by app version.

Date and scope: Original Your Phone studies 2019/2021; app 1.21011.127.0 in 2021.

Sources: [phone-research](https://github.com/LabCIF/YPA/blob/b984ab0719e554926e1f46bd9f669ca3c6cc15d4/YPAFI.py)

## F088: original PDF page 76 (printed 75)

Category: factual error

Original:

because it can prove a site was visited even after browsing history has been cleared

Replacement:

because icons can survive cleared history, without proving a visit

Reason: Icons can originate from sources other than direct visits.

Date and scope: Original Chromium favicon implementation from a 2025 release.

Sources: [chromium-favicons](https://github.com/chromium/chromium/blob/137.0.7151.119/components/favicon/core/favicon_service_impl.cc)

## F089: original PDF page 77 (printed 76)

Category: factual error

Original:

All of Edge's timestamps, in this database and elsewhere in its profile, use the same epoch as

Replacement:

The History database timestamps described here use the same epoch as

Reason: The convention is not universal for every Edge profile timestamp.

Date and scope: Original Chromium base::Time/History implementation, 2025 release.

Sources: [chromium-time](https://github.com/chromium/chromium/blob/137.0.7151.119/base/time/time.h); [chromium-history](https://github.com/chromium/chromium/blob/137.0.7151.119/components/history/core/browser/visit_database.cc)

## F090: original PDF page 79 (printed 78)

Category: factual error

Original:

%AppData% \Microsoft\Windows\Notifications\wpndatabase.db

Replacement:

%LocalAppData%\Microsoft\Windows\Notifications\wpndatabase.db

Reason: Second Local/Roaming path error.

Date and scope: Original Dissect parser 2026-06-10; notification research January 2022.

Sources: [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F091: original PDF page 81 (printed 80)

Category: factual error

Original:

broadly, when cloud sync is fully enabled, up to 4 megabytes per item and up to 25 items can sync to the account cloud

Replacement:

local history supports up to 25 items of up to 4 MB each; cross-device sync supports text below 100 KB

Reason: Local limits were assigned to cloud sync.

Date and scope: Microsoft 2018-10-02 announcement; support ms.date 2026-06-05.

Sources: [clipboard](https://support.microsoft.com/en-US/Windows/Apps/using-the-clipboard); [Find out what’s new in Windows and Office in October](https://blogs.windows.com/windowsexperience/2018/10/02/find-out-whats-new-in-windows-and-office-in-october/)

## F092: original PDF page 81 (printed 80)

Category: factual error

Original:

its content as RTF text

Replacement:

its text content

Reason: Modern Note.Text is not generally the legacy RTF format.

Date and scope: Original Sticky Notes SQL parser before cutoff.

Sources: [sticky-parser](https://github.com/kacos2000/Win10/blob/d39f62d323b320bf55cd2e9c643aa3feaed54eb8/StickyNotes/StickyNotes_plum_sqlite.sql)

## F093: original PDF page 81 (printed 80)

Category: factual error

Original:

a companion Media table stores any images embedded directly inside a note as binary blobs

Replacement:

a companion Media table references images stored in the app's local media folder

Reason: Media.LocalFileRelativePath refers to separate files.

Date and scope: Original Sticky Notes schema/query before cutoff.

Sources: [sticky-parser](https://github.com/kacos2000/Win10/blob/d39f62d323b320bf55cd2e9c643aa3feaed54eb8/StickyNotes/StickyNotes_plum_sqlite.sql)

## F094: original PDF page 84 (printed 83)

Category: factual error

Original:

setting it to a non-zero value is how a callback denies the process creation entirely

Replacement:

setting it to an error status is how a callback denies process creation

Reason: Nonzero NTSTATUS does not necessarily mean failure.

Date and scope: Microsoft PS_CREATE_NOTIFY_INFO 2023-01-13.

Sources: [PS_CREATE_NOTIFY_INFO (ntddk.h) - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_ps_create_notify_info)

## F095: original PDF page 85 (printed 84)

Category: factual error

Original:

The undocumented Ex variant, observed on some Windows builds, receives a notification type and, in some cases, the thread's actual start address.

Replacement:

The documented Ex registration API, available since Windows 10, takes a notification type. Its callback still receives process ID, thread ID, and a create/delete flag, without a start address.

Reason: Documented API and callback signature were misdescribed.

Date and scope: Microsoft DDI page 2022-03-16; minimum Windows 10.

Sources: [PsSetCreateThreadNotifyRoutineEx function (ntddk.h) - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutineex)

## F096: original PDF page 86 (printed 85)

Category: factual error

Original:

"post" notifications, which fire afterward purely for observation

Replacement:

"post" notifications, which fire afterward and can modify output parameters or the returned status

Reason: Post-notification may modify results.

Date and scope: Microsoft documents post-result modification since Vista.

Sources: [Handling Notifications - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/handling-notifications)

## F097: original PDF page 87 (printed 86)

Category: factual error

Original:

antivirus products cluster at the very

Replacement:

the highest FSFilter group sits near the

Reason: 400000–409999 is FSFilter Top.

Date and scope: Microsoft groups table frozen before July 2026.

Sources: [Load Order Groups and Altitudes for Minifilter Drivers - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)

## F098: original PDF page 88 (printed 87)

Category: factual error

Original:

top, from 400000 to 409999 for the highest tier down through 320000 to 329999 for a broader antivirus and EDR band

Replacement:

top, from 400000 to 409999 for FSFilter Top; 320000 to 329999 is the FSFilter AntiVirus range

Reason: Correct category names, retaining numerical coverage.

Date and scope: Microsoft group definitions frozen before cutoff.

Sources: [Load Order Groups and Altitudes for Minifilter Drivers - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)

## F099: original PDF page 88 (printed 87)

Category: version-dependent behavior

Original:

near the very bottom, at altitude 45000, sits FileInfo.sys , which captures the file metadata used to populate the MFT and represents the lowest point in the stack where file operations can still be reliably intercepted before they reach the disk itself.

Replacement:

FileInfo.sys has a legacy assigned altitude of 40500 and a newer assignment of 360500.5. It supplies file information; NTFS maintains the MFT. Lower-altitude filters can also exist.

Reason: Wrong altitude, MFT ownership, and absolute lowest-point claim.

Date and scope: Microsoft table frozen 2026-06-30 includes both assignments; exact introduction date not established, documented by cutoff.

Sources: [Allocated Filter Altitudes - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ifs/allocated-altitudes); [Master File Table (Local File Systems) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/fileio/master-file-table)

## F100: original PDF page 89 (printed 88)

Category: factual error

Original:

with its identifying GUID published under

Replacement:

with manifest-based providers registered under

Reason: TraceLogging providers do not require registered manifests.

Date and scope: Microsoft TraceLogging documentation predates cutoff.

Sources: [EVENT_DESCRIPTOR (evntprov.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/evntprov/ns-evntprov-event_descriptor); [About TraceLogging - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/tracelogging/trace-logging-about)

## F101: original PDF page 97 (printed 96)

Category: factual error

Original:

meaning it won't show up in that console at all unless you know to go looking for it in the raw file structure or the registry cache covered in the next chapter.

Replacement:

meaning it can be omitted from the default console view; View > Show Hidden Tasks reveals it.

Reason: Normal console can display hidden tasks.

Date and scope: Task Scheduler 2.0 Hidden property since Vista.

Sources: [TaskSettings.Hidden property - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/taskschd/tasksettings-hidden)

## F102: original PDF page 100 (printed 99)

Category: version-dependent behavior

Original:

almost all of them hidden from the ordinary Task Scheduler view

Replacement:

with names, schedules, visibility, and availability varying by build and configuration

Reason: Do not assert a universal hidden roster; individual unverified schedules flagged separately.

Date and scope: Task Scheduler Hidden property since Vista; task-cache research 2022-06-01.

Sources: [TaskSettings.Hidden property - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/taskschd/tasksettings-hidden); [tasks-research](https://cyber.wtf/2022/06/01/windows-registry-analysis-todays-episode-tasks/)

## F103: original PDF page 101 (printed 100)

Category: factual error

Original:

with a parallel mirror at %SystemRoot% \SysWOW64\Tasks\ for 32-bit tasks on a 64-bit system, and a legacy .job -format folder still supported at %AppData% \Microsoft\Windows\Task\ for backward compatibility.

Replacement:

shared by 32-bit and 64-bit tasks; legacy Task Scheduler 1.0 .job files use %SystemRoot%\Tasks\.

Reason: No separate SysWOW64 task namespace; wrong legacy path.

Date and scope: Microsoft Task Scheduler storage/compatibility documentation since Vista.

Sources: [Task Scheduler for developers - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page)

## F104: original PDF page 101 (printed 100)

Category: factual error

Original:

an event trigger driven by a WQL event subscription, the same query language used by WMI persistence mechanisms covered in part ten

Replacement:

an event trigger driven by an XPath query over Windows Event Log events

Reason: Event subscriptions use XPath, not WQL.

Date and scope: Microsoft Subscription schema element, Vista/Server 2008 minimum.

Sources: [Subscription (eventTriggerType) Element - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/taskschd/taskschedulerschema-subscription-eventtriggertype-element)

## F105: original PDF page 102 (printed 101)

Category: version-dependent behavior

Original:

a SHA-256 hash of the task's XML file

Replacement:

a version-dependent CRC32 or SHA-256 hash of the task's XML definition

Reason: Hash algorithm varies by version.

Date and scope: Original task-cache research 2022-06-01.

Sources: [tasks-research](https://cyber.wtf/2022/06/01/windows-registry-analysis-todays-episode-tasks/)

## F106: original PDF page 102 (printed 101)

Category: factual error

Original:

the FILETIME of its next scheduled run

Replacement:

the FILETIME of its last successful completion, when that field is present

Reason: DynamicInfo field is not next run.

Date and scope: Original Win10 1909 / Win7 research 2022-06-01.

Sources: [tasks-research](https://cyber.wtf/2022/06/01/windows-registry-analysis-todays-episode-tasks/)

## F107: original PDF page 102 (printed 101)

Category: factual error

Original:

Logon , Boot , Plain , and Volatile

Replacement:

Logon, Boot, Plain, and Maintenance

Reason: Wrong indexed category.

Date and scope: Original TaskCache structural research 2022-06-01.

Sources: [tasks-research](https://cyber.wtf/2022/06/01/windows-registry-analysis-todays-episode-tasks/)

## F108: original PDF page 103 (printed 102)

Category: factual error

Original:

202 marks the task as a whole finishing, after every one of its actions has run

Replacement:

102 marks successful completion of the task instance; 202 indicates an action failure

Reason: 202 is ActionFailure.

Date and scope: Original enum 2020-02-29 links Microsoft's original event documentation.

Sources: [task-events](https://github.com/dahall/TaskScheduler/blob/cce3ff7a1613d3d487ab8835711dfcb3480fadae/TaskService/TaskEvent.cs)

## F109: original PDF page 103 (printed 102)

Category: factual error

Original:

and, on Windows 11, event ID 322 specifically flags a task registered by a non-administrator account, while 325 records a task launch request being made

Replacement:

event ID 322 means a new instance was ignored because the task was already running, while 325 records an instance queued to launch immediately

Reason: Both event meanings wrong and not Windows 11 additions.

Date and scope: Original event enum pinned 2020-02-29.

Sources: [task-events](https://github.com/dahall/TaskScheduler/blob/cce3ff7a1613d3d487ab8835711dfcb3480fadae/TaskService/TaskEvent.cs)

## F110: original PDF page 105 (printed 104)

Category: factual error

Original:

isn't a destination for outbound data at all but a source the device pulls from

Replacement:

is primarily a configuration endpoint the device pulls from

Reason: A configuration download does not establish zero outbound request data.

Date and scope: Microsoft endpoint documentation 2026-06-16.

Sources: [Connection endpoints for Windows 11 Enterprise - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-windows-11-endpoints)

## F111: original PDF page 109 (printed 108)

Category: factual error

Original:

The actual sync state lives in a SQLite database, typically named SyncEngine.db or SyncEngineDatabase.db depending on version, whose schema varies somewhat across releases but consistently centers on a scope_items table: one row per file or folder ever known to OneDrive, recording a cloud item ID, its parent folder's ID, a SharePoint resource ID where relevant, name, size, a folder flag, created and modified timestamps, the local filesystem path, a cloud sync ETag, a JSON blob of content hashes (both SHA-1 and Microsoft's own QuickXorHash), a deleted flag, and conflict

Replacement:

The sync state can live in SyncEngineDatabase.db, whose tables vary by release. Versions parsed by OneDriveExplorer use od_ClientFile_Records, od_ClientFolder_Records, and od_ScopeInfo_Records for file, folder, and scope metadata. They can hold names, parent/resource IDs, sizes, status, ETags, timestamps, and local hashes. Check the actual tables: hash algorithms and hydration details vary, and the database need not hold a complete history. Transfer and deletion

Reason: The claimed stable scope_items schema is not the analyzed OneDrive schema.

Date and scope: Original OneDriveExplorer parser at commit dated 2025-09-20.

Sources: [onedrive-sqlite](https://github.com/Beercow/OneDriveExplorer/blob/7f8021e1b4128b5f027530af7e5952bfbda052c0/OneDriveExplorer/ode/parsers/sqlite_db.py)

## F112: original PDF page 110 (printed 109)

Category: factual error

Original:

information where applicable. Companion pending_upload and pending_download tables track files queued for transfer, including retry counts and error codes. Because scope_items records every file OneDrive has ever synced, deleted files included (flagged with is_deleted=1 ), and because its stored hash values remain useful for threat-intelligence lookups even after a file has been removed locally, this database is often one of the more productive artifacts in an investigation touching cloud-synced data.

Replacement:

information may be available in logs and state that vary by version. OneDriveExplorer also parses SafeDelete.db tables such as items_moved_to_recycle_bin and filter_delete_info. These can preserve deletion evidence, though a local database need not record every file ever synced. Retained hashes and metadata can still be useful after a local file is removed.

Reason: Unauthenticated table names and exhaustive history replaced with supported structures.

Date and scope: Original parser 2025-09-20.

Sources: [onedrive-sqlite](https://github.com/Beercow/OneDriveExplorer/blob/7f8021e1b4128b5f027530af7e5952bfbda052c0/OneDriveExplorer/ode/parsers/sqlite_db.py)

## F113: original PDF page 110 (printed 109)

Category: factual error

Original:

its $DATA attribute is empty aside from the reparse buffer itself

Replacement:

its $DATA can be unallocated; a separate $REPARSE_POINT holds the reparse buffer

Reason: Reparse buffer is not inside $DATA.

Date and scope: Microsoft NTFS/cloud-placeholder documentation predates cutoff.

Sources: [Reparse Points - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/fileio/reparse-points); [Cloud Sync Engines - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/cfapi/cloud-files-api-portal)

## F114: original PDF page 111 (printed 110)

Category: factual error

Original:

the local database keeps its own copy indefinitely, and cross-device clipboard items, capped at four

Replacement:

the local database also expires activity. Cloud clipboard supports text below 100 KB; local history supports items up to four

Reason: Timeline has expiry; cloud/local limits conflated.

Date and scope: Original Timeline parser 2023-02-16; Microsoft clipboard announcement 2018-10-02.

Sources: [timeline-parser](https://github.com/kacos2000/WindowsTimeline/blob/696293696cc5d6ed6b5c82cb61139883b6a6505b/README.md); [Find out what’s new in Windows and Office in October](https://blogs.windows.com/windowsexperience/2018/10/02/find-out-whats-new-in-windows-and-office-in-october/); [clipboard](https://support.microsoft.com/en-US/Windows/Apps/using-the-clipboard)

## F115: original PDF page 112 (printed 111)

Category: factual error

Original:

megabytes each, are retained only per-copy and clear as soon as a new item is copied.

Replacement:

megabytes each; history can retain multiple entries.

Reason: History is not the ordinary single-item clipboard.

Date and scope: Microsoft support ms.date 2026-06-05; history introduced 2018.

Sources: [clipboard](https://support.microsoft.com/en-US/Windows/Apps/using-the-clipboard)

## F116: original PDF page 114 (printed 113)

Category: factual error

Original:

with a partial hash of the URL itself, kept partial specifically for privacy reasons.

Replacement:

with URL and reputation information, rather than only a partial hash of the URL.

Reason: Microsoft describes URL information, not a partial-hash-only protocol.

Date and scope: Microsoft Windows 8 / Server 2012 privacy documentation.

Sources: [Manage Privacy: SmartScreen Filter and Resulting Internet Communication](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj618329(v=ws.11))

## F117: original PDF page 114 (printed 113)

Category: factual error

Original:

(a process referred to as ELAM flagging, after the Early Launch Anti-Malware driver)

Replacement:

(subject to cloud-protection and sample-submission settings)

Reason: ELAM classifies boot-start drivers, not this sample-submission mechanism.

Date and scope: ELAM since Windows 8; Defender CSP 2026-06-22.

Sources: [ELAM Driver Requirements - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/elam-driver-requirements); [Defender Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-defender)

## F118: original PDF page 114 (printed 113)

Category: version-dependent behavior

Original:

a value of 1 enables "Basic" membership, sending only hashes and metadata, while a value of 2 enables "Advanced" membership, which permits full sample submission

Replacement:

on Windows 10 and later, values of either 1 or 2 select Advanced membership; the older Basic distinction no longer applies

Reason: Basic is no longer a hash-only mode.

Date and scope: Microsoft explicitly identifies Windows 10 change; CSP dated 2026-06-22.

Sources: [Defender Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-defender)

## F119: original PDF page 114 (printed 113)

Category: factual error

Original:

with sync fully enabled, both text and images up to four megabytes each, up to twenty-five items, sync to the Microsoft account cloud

Replacement:

with cloud sync enabled, text below 100 KB can sync; local history supports twenty-five items of up to four megabytes each

Reason: Repeated cloud/local limits error.

Date and scope: Microsoft announcement 2018-10-02; support ms.date 2026-06-05.

Sources: [Find out what’s new in Windows and Office in October](https://blogs.windows.com/windowsexperience/2018/10/02/find-out-whats-new-in-windows-and-office-in-october/); [clipboard](https://support.microsoft.com/en-US/Windows/Apps/using-the-clipboard)

## F120: original PDF page 115 (printed 114)

Category: version-dependent behavior

Original:

Network Location Awareness ( NlaSvc ).

Replacement:

NCSI, hosted by NlaSvc on Windows 10 and the Network List Service (netprofm) on Windows 11.

Reason: NCSI hosting changed in Windows 11.

Date and scope: Microsoft NCSI source frozen before July 2026 explicitly states Windows 11 change.

Sources: [Network Connection Status Indicator (NCSI) troubleshooting guidance - Windows Server](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/troubleshoot-ncsi-guidance)

## F121: original PDF page 116 (printed 115)

Category: factual error

Original:

as FILETIME values

Replacement:

as 16-byte SYSTEMTIME values

Reason: NetworkList uses eight little-endian 16-bit fields.

Date and scope: Original parser change history 2009-08-12; pinned 2024-11-15.

Sources: [networklist-parser](https://github.com/keydet89/RegRipper3.0/blob/8f54a2c4f61aa3dee60271b97bdf855cca60a054/plugins/networklist.pl)

## F122: original PDF page 119 (printed 118)

Category: factual error

Original:

xbgm for the Xbox Game Bar overlay

Replacement:

xbgm for Xbox Game Monitoring

Reason: The original CIS benchmark identifies xbgm as Xbox Game Monitoring. This is a legacy, build-dependent service name, not Game Bar itself.

Date and scope: CIS Windows 10 Release 1703 benchmark announcement, 2017-11-06.

Sources: [Update: CIS Microsoft Windows 10 Enterprise (Release 1703) Benchmark v1.0.0](https://www.cisecurity.org/insights/blog/update-cis-microsoft-windows-10-enterprise-release-1703-benchmark-v1-0-0)

## F123: original PDF page 120 (printed 119)

Category: factual error

Original:

a WMI-based LicenseManager component

Replacement:

LicenseManager

Reason: LicenseManager is a Windows service.

Date and scope: Microsoft Windows Server service guidance before cutoff.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server)

## F124: original PDF page 124 (printed 123)

Category: factual error

Original:

older systems used a simpler jobs.xml

Replacement:

older systems used qmgr0.dat and qmgr1.dat

Reason: Wrong legacy BITS filenames.

Date and scope: Mandiant original BITS research 2021; migrated Google Cloud article 2024-03-26.

Sources: [Attacker Use Background Intelligent Transfer Service (BITS) | Google Cloud Blog](https://cloud.google.com/blog/topics/threat-intelligence/attacker-use-of-windows-background-intelligent-transfer-service)

## F125: original PDF page 124 (printed 123)

Category: factual error

Original:

4 for a job being modified

Replacement:

4 for a job completing

Reason: BITS event 4 is job completion.

Date and scope: Original Windows 10 17134 provider manifest (2018).

Sources: [bits-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-Bits-Client.xml)

## F126: original PDF page 124 (printed 123)

Category: factual error

Original:

60 for it completing

Replacement:

60 for transfer stop

Reason: Stopping need not mean success.

Date and scope: Original Windows 10 17134 manifest (2018).

Sources: [bits-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-Bits-Client.xml)

## F127: original PDF page 59 (printed 58)

Category: factual error

Original:

logs job creation, start, and completion (event IDs 3, 59, and 60)

Replacement:

logs job creation, transfer start, and transfer stop (event IDs 3, 59, and 60)

Reason: First occurrence of same BITS event 60 error.

Date and scope: Original Windows 10 17134 manifest (2018).

Sources: [bits-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-Bits-Client.xml)

## F128: original PDF page 59 (printed 58)

Category: factual error

Original:

logs new RDP connections and connection closures (event IDs 131 and 98)

Replacement:

logs accepted and established TCP connections (event IDs 131 and 98)

Reason: 98 is establishment, not closure.

Date and scope: Original Windows 10 17134 provider manifest (2018).

Sources: [rdp-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-RemoteDesktopServices-RdpCoreTS.xml)

## F129: original PDF page 125 (printed 124)

Category: factual error

Original:

running before essentially every other defense on the machine is even awake

Replacement:

running before ordinary user-mode defenses, though kernel protections such as ELAM initialize earlier

Reason: BootExecute does not precede ELAM.

Date and scope: Microsoft ELAM design since Windows 8.

Sources: [ELAM Driver Requirements - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/elam-driver-requirements)

## F130: original PDF page 126 (printed 125)

Category: factual error

Original:

accumulates a complete history of every storage volume Windows has ever assigned a drive letter to, and it never cleans old entries out on its own.

Replacement:

stores persistent volume identities and drive-letter mappings, which can outlast connections but do not form a complete assignment history.

Reason: Mappings can be replaced or removed.

Date and scope: Microsoft Mount Manager design before cutoff.

Sources: [Supporting Mount Manager Requests in a Storage Class Driver - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)

## F131: original PDF page 126 (printed 125)

Category: factual error

Original:

Because this key never forgets a drive letter assignment

Replacement:

Because volume IDs can persist

Reason: Remove repeated exhaustive-history guarantee.

Date and scope: Microsoft Mount Manager source frozen before cutoff.

Sources: [Supporting Mount Manager Requests in a Storage Class Driver - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)

## F132: original PDF page 127 (printed 126)

Category: factual error

Original:

self-deletes each entry immediately after it runs once

Replacement:

normally deletes entries before execution; ! defers deletion until afterward

Reason: Deletion order reversed.

Date and scope: Microsoft Run/RunOnce documentation includes XP/Vista/Windows 7.

Sources: [Run and RunOnce Registry Keys - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/setupapi/run-and-runonce-registry-keys)

## F133: original PDF page 130 (printed 129)

Category: factual error

Original:

5858 marks one failing

Replacement:

5858 records a failed WMI client operation

Reason: Not exclusively provider startup failure.

Date and scope: Microsoft article applies to Server 2012 R2; frozen pre-cutoff.

Sources: [WMI-Activity Event 5858 ResultCode 0x80041032 - Windows Client](https://learn.microsoft.com/en-us/troubleshoot/windows-client/system-management-components/wmi-activity-event-5858-logged-with-resultcode-0x80041032)

## F134: original PDF page 130 (printed 129)

Category: factual error

Original:

event IDs 5860 and 5861, marking a permanent event consumer and a permanent event filter being registered respectively

Replacement:

event IDs 5860 and 5861, marking temporary event subscriptions and permanent filter-to-consumer bindings respectively

Reason: Both subscription meanings wrong.

Date and scope: Original Windows 10 17134 WMI provider manifest (2018).

Sources: [wmi-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-WMI-Activity.xml)

## F135: original PDF page 132 (printed 131)

Category: factual error

Original:

the classic Windows PowerShell.evtx log

Replacement:

the Microsoft-Windows-PowerShell/Operational log

Reason: 4103 uses Operational channel.

Date and scope: Windows 10 17134 manifest (2018); Microsoft reference before cutoff.

Sources: [powershell-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-PowerShell.xml); [about_Logging_Windows - PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-5.1)

## F136: original PDF page 133 (printed 132)

Category: factual error

Original:

PowerShell logs the script block's content after its own parser has expanded and deobfuscated it, which means even a script wrapped in Base64 through -EncodedCommand , or heavily string-concatenated to defeat simple pattern matching, still gets logged in its final, readable form.

Replacement:

PowerShell can log decoded -EncodedCommand text and script blocks created during execution. Some obfuscated expressions still need analysis; the log does not always show their final result.

Reason: Not a universal deobfuscation engine.

Date and scope: Original PowerShell implementation and documentation before cutoff.

Sources: [about_Logging_Windows - PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-5.1); [powershell-sbl](https://github.com/PowerShell/PowerShell/blob/v7.4.0/src/System.Management.Automation/engine/runtime/CompiledScriptBlock.cs)

## F137: original PDF page 133 (printed 132)

Category: factual error

Original:

with an optional invocation header recording exactly when the session started

Replacement:

with an optional invocation header recording timestamps for individual commands

Reason: Ordinary session header already timestamps session start.

Date and scope: Microsoft Start-Transcript IncludeInvocationHeader, PowerShell 5.1.

Sources: [Start-Transcript (Microsoft.PowerShell.Host) - PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.host/start-transcript?view=powershell-5.1)

## F138: original PDF page 134 (printed 133)

Category: factual error

Original:

essentially everything typed interactively into a PowerShell console

Replacement:

interactive commands retained by PSReadLine, subject to history settings and sensitive-data filtering

Reason: Sensitive commands can be filtered; history can be disabled.

Date and scope: Microsoft release notes: 2.0.4 (2020-08-05), 2.1 (2020-11-02).

Sources: [about_PSReadLine_Release_Notes - PowerShell](https://learn.microsoft.com/en-us/powershell/module/psreadline/about/about_psreadline_release_notes)

## F139: original PDF page 135 (printed 134)

Category: factual error

Original:

a cached entry proves a domain-name resolution was attempted

Replacement:

a cached entry may reflect a query or a Hosts-file preload

Reason: Cache can include preloaded Hosts entries.

Date and scope: Microsoft ipconfig /displaydns documentation before cutoff.

Sources: [ipconfig](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig)

## F140: original PDF page 136 (printed 135)

Category: factual error

Original:

8 is network logon with credentials passed in clear text

Replacement:

8 is NetworkCleartext (not necessarily plaintext on the wire)

Reason: NetworkCleartext does not establish plaintext on the wire.

Date and scope: Microsoft event 4624 documentation 2021-09-07.

Sources: [4624(S) An account was successfully logged on. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624)

## F141: original PDF page 137 (printed 136)

Category: factual error

Original:

an event that (fortunately) it is not possible to suppress from being logged, since the act of clearing the log is itself what triggers it.

Replacement:

an event generated by normal Security-log clearing regardless of audit policy. Offline deletion or other tampering may leave no such event.

Reason: Normal clearing logs 1102; it is not indestructible evidence.

Date and scope: Microsoft event 1102 documentation 2021-09-07.

Sources: [1102(S) The audit log was cleared. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-1102)

## F142: original PDF page 138 (printed 137)

Category: factual error

Original:

an audit-mode "allowed" event and a genuinely permitted execution look identical apart from that one setting

Replacement:

different event IDs and messages identify allowed executions and those that would have been blocked in audit mode

Reason: 8003/8006 differ from 8002/8005.

Date and scope: Microsoft event table 2024-09-11, updated 2025-02-24.

Sources: [Using Event Viewer with AppLocker](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/applocker/using-event-viewer-with-applocker)

## F143: original PDF page 140 (printed 139)

Category: factual error

Original:

a Windows Hello PIN never leaves the TPM

Replacement:

a Hello PIN never leaves the device

Reason: PIN device-bound; TPM is not a universal boundary.

Date and scope: Microsoft Windows 11 Security Book, September 2023; software keys also supported.

Sources: [Microsoft Windows 11 Security Book](https://www.microsoft.com/content/dam/microsoft/final/en-us/microsoft-brand/documents/MSFT-Windows11-Security-book_Sept2023.pdf)

## F144: original PDF page 141 (printed 140)

Category: factual error

Original:

Recall's screenshots, or a browser's stored logins

Replacement:

application secrets, or a browser's stored logins

Reason: Make DPAPI overview consistent with corrected Recall architecture.

Date and scope: Microsoft architecture 2024-09-27.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)

## F145: original PDF page 141 (printed 140)

Category: factual error

Original:

reduces to a single per-user master key, and understanding where that key lives and how it's derived

Replacement:

uses user or SYSTEM master keys. Understanding where those keys live and how they're derived

Reason: Multiple master-key GUIDs and SYSTEM context exist.

Date and scope: Original parser and format implementation pinned 2026-06-10.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py)

## F146: original PDF page 141 (printed 140)

Category: factual error

Original:

%ProgramData%\Microsoft\Protect\S-1-5-18

Replacement:

%SystemRoot%\System32\Microsoft\Protect\S-1-5-18

Reason: Wrong SYSTEM master-key directory.

Date and scope: Parser 2026-06-10; SpecterOps 2026-03-04, modified 2026-06-17.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py); [Offensive DPAPI With Nemesis](https://specterops.io/blog/2026/03/04/offensive-dpapi-with-nemesis/)

## F147: original PDF page 141 (printed 140)

Category: factual error

Original:

requires deriving an intermediate key from the user's own password, run through repeated SHA-1 hashing and a PBKDF2-style key derivation combined with the user's SID acting as part of the input, before the result can be used to decrypt the actual master key blob with AES.

Replacement:

depends on the account and key-file format. A password-derived credential and the user's SID help unlock user keys; the file records the derivation settings and cipher. Modern files commonly use AES; older formats differ.

Reason: Not a universal repeated-SHA1/AES derivation chain.

Date and scope: Original implementation pinned 2026-06-10, with Windows 10 fixtures.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py); [dpapi-masterkey](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/master_key.py)

## F148: original PDF page 142 (printed 141)

Category: factual error

Original:

to a Recall screenshot's encryption

Replacement:

to other DPAPI-protected application secrets

Reason: Second DPAPI/Recall contradiction.

Date and scope: Microsoft architecture 2024-09-27.

Sources: [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)

## F149: original PDF page 142 (printed 141)

Category: factual error

Original:

any domain user's master key directly

Replacement:

domain-user master keys containing matching domain-backup recovery data

Reason: Recovery key is not a universal decryptor for every master-key context.

Date and scope: Microsoft backup-key documentation and original parser before cutoff.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py); [DPAPI backup keys on Active Directory domain controllers - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/seccng/cng-dpapi-backup-keys-on-ad-domain-controllers)

## F150: original PDF page 143 (printed 142)

Category: factual error

Original:

a simple XOR against a fixed byte value

Replacement:

RC4 encryption using a fixed key

Reason: Defender quarantine uses RC4.

Date and scope: Original Dissect implementation 2026-06-10.

Sources: [quarantine-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/defender/quarantine.py)

## F151: original PDF page 143 (printed 142)

Category: factual error

Original:

Beyond the AMSI-specific event IDs covered in chapter 35, Defender's operational event log also records event ID 1006 for a general malware detection

Replacement:

The 1116/1117 events covered in chapter 35 are general Defender detection/action events, also used for AMSI detections; older event sets include 1006

Reason: 1116/1117 are not exclusive to AMSI; 1006 is legacy.

Date and scope: Microsoft event documentation 2026-05-11, updated 2026-06-01.

Sources: [Microsoft Defender Antivirus event IDs and error codes - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-microsoft-defender-antivirus)

## F152: original PDF page 145 (printed 144)

Category: factual error

Original:

for every packet it evaluates

Replacement:

for the dropped packets and successful connections selected for logging

Reason: Not every evaluated packet is logged.

Date and scope: Microsoft documentation 2018-05-31.

Sources: [Troubleshooting Firewall-Related Issues](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ics/troubleshooting-firewall-related-issues)

## F153: original PDF page 147 (printed 146)

Category: factual error

Original:

caches a copy of every .msi package ever installed, renamed to a GUID-based filename that no longer resembles the original

Replacement:

caches local copies of installed .msi packages, often stripped of embedded cabinets and renamed to internal filenames

Reason: Cache is not a permanent archive of every package or a GUID filename scheme.

Date and scope: Microsoft installer engineering 2005-11-29.

Sources: [Windows Installer Cache](https://devblogs.microsoft.com/setup/windows-installer-cache/)

## F154: original PDF page 148 (printed 147)

Category: factual error

Original:

3 for manual start only

Replacement:

3 for demand start, including service triggers

Reason: Demand start is not manual-only.

Date and scope: Microsoft start types and service-trigger design since Windows 7.

Sources: [HKLM\SYSTEM\CurrentControlSet\Services Registry Tree - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree); [Service Trigger Events - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/services/service-trigger-events)

## F155: original PDF page 149 (printed 148)

Category: factual error

Original:

event ID 1500 marks processing starting, 1501 marks it completing successfully, and 1502 marks a failure along with an error code identifying what went wrong.

Replacement:

4000/4001 mark computer/user policy processing starting, and 8000/8001 mark successful completion; failures use other event IDs.

Reason: Incorrect GroupPolicy Operational event sequence.

Date and scope: Microsoft engineering article migrated by 2019-08-29.

Sources: [Is Group Policy Slowing Me Down? | Microsoft Community Hub](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/is-group-policy-slowing-me-down/ba-p/259701/)

## F156: original PDF page 150 (printed 149)

Category: factual error

Original:

typically capped at sixty-four per file before the log rolls over to reuse the oldest ones

Replacement:

each 64 KiB, with the chunk count depending on log size

Reason: 64 refers to KiB/chunk, not a maximum chunk count.

Date and scope: Original EVTX specification 2024-09-27.

Sources: [evtx-spec](https://github.com/libyal/libevtx/blob/22e208e4837786c4c88e1c7679357d66bb4c6c90/documentation/Windows%20XML%20Event%20Log%20%28EVTX%29.asciidoc)

## F157: original PDF page 151 (printed 150)

Category: factual error

Original:

a MaxSize value under HKLM\SYSTEM\CurrentControlSet\Services\EventLog\{ChannelName}\

Replacement:

a maximum log size (MaxSize under HKLM\SYSTEM\CurrentControlSet\Services\EventLog\{LogName}\ for classic logs)

Reason: The classic registry layout must not be presented as the configuration path for every modern channel. Retain the correct classic path and limit its scope; do not substitute an unverified modern registry path.

Date and scope: Classic Eventlog documentation dated 2021-01-07; Windows Event Log channel API available since Vista / Server 2008.

Sources: [Eventlog Key - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/eventlog/eventlog-key); [EVT_CHANNEL_CONFIG_PROPERTY_ID (winevt.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winevt/ne-winevt-evt_channel_config_property_id)

## F158: original PDF page 151 (printed 150)

Category: factual error

Original:

is itself always logged as event ID 1102

Replacement:

normally generates event ID 1102

Reason: Remove repeated guarantee against offline tampering.

Date and scope: Microsoft 1102 documentation 2021-09-07.

Sources: [1102(S) The audit log was cleared. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-1102)

## F159: original PDF page 154 (printed 153)

Category: factual error

Original:

its hibernation-file plugin for pulling a usable memory image out of hiberfil.sys

Replacement:

hibernation-layer or conversion support, which depends on version

Reason: Do not assume a standard generally available plugin.

Date and scope: Volatility contributor discussion 2025-10-07/08.

Sources: [Image copy · Issue #1887 · volatilityfoundation/volatility3](https://github.com/volatilityfoundation/volatility3/issues/1887)

## F160: original PDF page 157 (printed 156)

Category: factual error

Original:

genuinely defeats recovery of that content from $MFT slack or $Recycle.Bin (chapter 13)

Replacement:

can defeat recovery from overwritten blocks, but not other copies or remapped SSD blocks

Reason: Overwriting a file is not a universal sanitization guarantee.

Date and scope: NIST SP 800-88 Rev.1, December 2014; Microsoft SDelete before cutoff.

Sources: [SDelete - Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/sdelete); [NIST Special Publication (SP) 800-88 Rev. 1 (Withdrawn), Guidelines for Media Sanitization](https://csrc.nist.gov/pubs/sp/800/88/r1/final)

## F161: original PDF page 158 (printed 157)

Category: factual error

Original:

triggers event ID 1102 as an unavoidable side effect of the clearing action itself

Replacement:

normally triggers event ID 1102 when cleared through the running Event Log service

Reason: Third absolute guarantee about 1102.

Date and scope: Microsoft event documentation 2021-09-07.

Sources: [1102(S) The audit log was cleared. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-1102)

## F162: original PDF page 158 (printed 157)

Category: factual error

Original:

script block logging captures the fully deobfuscated command content specifically because logging happens after PowerShell's own parser has already unwound any encoding

Replacement:

enabled script block logging can capture decoded or dynamically executed script content, without guaranteeing complete deobfuscation

Reason: Repeated guarantee; logging also must be enabled.

Date and scope: Original implementation and Microsoft documentation before cutoff.

Sources: [about_Logging_Windows - PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-5.1); [powershell-sbl](https://github.com/PowerShell/PowerShell/blob/v7.4.0/src/System.Management.Automation/engine/runtime/CompiledScriptBlock.cs)

## F163: original PDF page 158 (printed 157)

Category: factual error

Original:

Disabling telemetry services like DiagTrack stops new data from reaching Microsoft going forward

Replacement:

Disabling DiagTrack stops its uploads, while other components can still contact Microsoft

Reason: DiagTrack does not gate every Microsoft-bound data flow.

Date and scope: Microsoft Windows component connections guidance 2026-02-12.

Sources: [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services); [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F164: original PDF page 159 (printed 158)

Category: factual error

Original:

registry-backed WMI repository

Replacement:

file-backed WMI repository

Reason: WMI repository is in files, not registry.

Date and scope: Microsoft architecture before cutoff; consistent with chapter 34.

Sources: [WMI Architecture - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmi-architecture)

## F165: original PDF page 160 (printed 159)

Category: version-dependent behavior

Original:

a value of 0 restricts collection to the Security level available only on Enterprise and Education editions, 1 sets it to Basic, 2 to Enhanced, and 3 to Full

Replacement:

0 means off on Enterprise/Education/Server; 1 is Required (Basic), 3 Optional (Full); 2 (Enhanced) is only for Windows 10 1809 or earlier and Server 2016/2019

Reason: Wrong edition restriction and level version support.

Date and scope: Microsoft documentation updated 2025-11-07; Enhanced only Win10 1809 and earlier, Server 2016/2019.

Sources: [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F166: original PDF page 160 (printed 159)

Category: factual error

Original:

either through sc config DiagTrack start=disabled or the equivalent PowerShell Set-Service command, which halts the local collection pipeline entirely regardless of the telemetry level setting.

Replacement:

using sc.exe stop DiagTrack, then sc.exe config DiagTrack start= disabled (or PowerShell Stop-Service and Set-Service); startup configuration alone does not stop a running service or other data flows.

Reason: Space after = required; sc can be a PowerShell alias; configuring is not stopping.

Date and scope: Microsoft sc.exe and service-control references before cutoff. Commands are text only and were not executed.

Sources: [sc.exe config](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-config); [Stopping a Service - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/services/stopping-a-service); [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)

## F167: original PDF page 161 (printed 160)

Category: factual error

Original:

HKLM\SOFTWARE\Policies\Microsoft\Windows\CurrentVersion\AdvertisingInfo\DisabledByGroupPolicy

Replacement:

HKLM\SOFTWARE\Policies\Microsoft\Windows\AdvertisingInfo\DisabledByGroupPolicy

Reason: Extra CurrentVersion component invalidates policy path.

Date and scope: Microsoft guidance 2026-02-12.

Sources: [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)

## F168: original PDF page 161 (printed 160)

Category: factual error

Original:

at the machine level, or the per-user TailoredExperiencesWithDiagnosticDataEnabled value, which also governs whether Microsoft uses your diagnostic data to personalize tips and suggestions more broadly.

Replacement:

at the machine level. TailoredExperiencesWithDiagnosticDataEnabled separately controls per-user diagnostic-data personalization of tips and suggestions.

Reason: Advertising ID and tailored experiences are separate controls.

Date and scope: Microsoft guidance 2026-02-12.

Sources: [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)

## F169: original PDF page 161 (printed 160)

Category: factual error

Original:

HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsAI\IsEnabled

Replacement:

HKCU\SOFTWARE\Policies\Microsoft\Windows\WindowsAI\DisableAIDataAnalysis=1

Reason: Second unsupported Recall control.

Date and scope: DisableAIDataAnalysis is identified in Microsoft Recall documentation dated 2025-12-02; its Windows 11 24H2 applicability starts with KB5055627 (April 2025). The current CSP page is used only for this existing policy mapping, not its later additions.

Sources: [WindowsAI Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai); [Manage Recall for Windows clients](https://learn.microsoft.com/en-us/windows/client-management/manage-recall); [Recall overview - Windows apps](https://learn.microsoft.com/en-us/windows/apps/develop/windows-integration/recall/)

## F170: original PDF page 161 (printed 160)

Category: factual error

Original:

SpynetReporting value governing Basic versus Advanced membership, alongside a separate policy specifically for the browser and app-level SmartScreen check under HKLM\SOFTWARE\Policies\Microsoft\Windows Defender\ .

Replacement:

SpynetReporting value for MAPS (1 and 2 both select Advanced on Windows 10 and later). SmartScreen has separate policies, including EnableSmartScreen under HKLM\SOFTWARE\Policies\Microsoft\Windows\System and SmartScreenEnabled under Microsoft Edge's policy key.

Reason: Basic distinction obsolete; wrong common SmartScreen policy location.

Date and scope: Defender CSP 2026-06-22; SmartScreen policy documentation predates cutoff.

Sources: [Defender Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-defender); [SmartScreen Policy CSP](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-smartscreen)

## F171: original PDF page 162 (printed 161)

Category: factual error

Original:

None of these settings retroactively erase what's already been collected and stored, whether that's already sitting in a local cache file or already uploaded to Microsoft. What they do is stop the collection going forward, which is exactly the distinction this book has drawn from its opening chapter onward: between the local artifact, which persists as a byproduct of how Windows works, and the telemetry upload, which is a separate, deliberate choice that these settings actually govern. Turning a service off tomorrow does not erase what it already wrote today, and by now, forty-three chapters in, you know exactly where to look to check.

Replacement:

Most of these settings do not erase existing local caches or data already uploaded to Microsoft. Recall's turn-off-snapshots policy also deletes saved snapshots. These controls affect particular forms of collection or upload; their scope depends on the setting and Windows version. That's the distinction this book has drawn from its opening chapter onward: between the local artifact, which persists as a byproduct of how Windows works, and the telemetry upload, which is a separate, deliberate choice that these settings govern. Turning a service off tomorrow does not erase what it already wrote today, and by now, forty-three chapters in, you know exactly where to look to check.

Reason: Recall's documented disable-snapshots policy deletes existing snapshots. Other controls have individual collection/upload scopes and must not be described as stopping every form of collection.

Date and scope: Microsoft Recall management documentation 2025-12-10; Microsoft connections guidance 2026-02-12; diagnostic-data documentation 2025-09-11.

Sources: [Manage Recall for Windows clients](https://learn.microsoft.com/en-us/windows/client-management/manage-recall); [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services); [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F172: original PDF page 13 (printed 12)

Category: factual error

Original:

but DiagTrack itself runs as long as your

Replacement:

and the minimum level depends on your

Reason: A diagnostic-data setting is not a guarantee that a Windows service is running; connect the edition qualification over the page break.

Date and scope: Microsoft diagnostic-data configuration documentation updated 2025-11-07.

Sources: [Configure Windows diagnostic data in your organization - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

## F173: original PDF page 21 (printed 20)

Category: factual error

Original:

determines whether a network is public, private, or domain-joined by probing www.msftconnecttest.com

Replacement:

tracks network context; NCSI tests internet reachability

Reason: Internet reachability probing is distinct from identifying network category.

Date and scope: Microsoft NCSI documentation frozen before July 2026 describes separate roles.

Sources: [Network Connection Status Indicator (NCSI) troubleshooting guidance - Windows Server](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/troubleshoot-ncsi-guidance)

## F174: original PDF page 73 (printed 72)

Category: factual error

Original:

a flag for whether the row itself originated from a cloud sync rather than locally

Replacement:

a cloud-creation timestamp where present

Reason: CreatedInCloud is a timestamp, not a universal Boolean flag.

Date and scope: Original ActivitiesCache parser pinned 2026-06-10.

Sources: [activities-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/activitiescache.py)

## F175: original PDF page 51 (printed 50)

Category: factual error

Original:

isn't accessible through ordinary Windows APIs at all; reading it requires raw access to the volume itself

Replacement:

isn't an ordinary user file; raw-volume access or NTFS control calls can retrieve its records

Reason: FSCTL_GET_NTFS_FILE_RECORD is a documented Win32 control call.

Date and scope: Microsoft API reference supports Windows XP and later; pre-cutoff source.

Sources: [FSCTL_GET_NTFS_FILE_RECORD - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winioctl/ni-winioctl-fsctl_get_ntfs_file_record)

## F176: original PDF page 140 (printed 139)

Category: factual error

Original:

keeping key material under %AppData%\Microsoft\Crypto\Ngc\ for a per-user key or the equivalent %ProgramData% location for a machine-context key

Replacement:

with key files under %SystemRoot%\ServiceProfiles\LocalService\AppData\Roaming\Microsoft\Crypto\Keys\ in the Windows 10 builds studied in 2021

Reason: The original Windows Hello study locates software key files in the LocalService profile, with separate Ngc metadata. Do not generalize the tested path to every provider.

Date and scope: Kim and Choi, original Windows 10 research published 2021-07-23, Table 2.

Sources: [Ejin Kim and Hyoung-Kee Choi: Security Analysis and Bypass User Authentication Bound to Device of Windows Hello in the Wild](https://onlinelibrary.wiley.com/doi/10.1155/2021/6245306)

## F177: original PDF page 23 (printed 22)

Category: factual error

Original:

a two-year rolling record

Replacement:

up to three years of records

Reason: Microsoft documents up to three years, not a two-year rolling limit.

Date and scope: UAL introduced in Windows Server 2012; Microsoft UAL documentation ms.date 2017-10-16, last updated 2026-02-16, immutable snapshot 2026-06-30.

Sources: [Get Started with User Access Logging](https://learn.microsoft.com/en-us/windows-server/administration/user-access-logging/get-started-with-user-access-logging)

## F178: original PDF page 23 (printed 22)

Category: factual error

Original:

a Current.mdb for the active year, GUID-named archives for prior years

Replacement:

a Current.mdb for daily activity, GUID-named databases for the current and prior years

Reason: The active annual data is held in a GUID-named database; Current.mdb is the daily staging database.

Date and scope: Microsoft Incident Response guide, 2024; its UAL section describes the daily copy into the current-year database.

Sources: [Microsoft Incident Response: Leveraging Windows Internals for Forensic Investigation](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/IR-Guidebook-Final.pdf)

## F179: original PDF page 19 (printed 18)

Category: outdated information

Original:

underlies Windows Timeline, cross-device clipboard, and Nearby Share, syncing to activityfeed.microsoft.com

Replacement:

supports cross-device features, including clipboard and Nearby sharing; older Timeline sync used activityfeed.microsoft.com

Reason: The endpoint must not imply current Timeline cloud synchronization, which ended before the cutoff.

Date and scope: Microsoft account activity-history cloud synchronization ended in 2021; Windows 11 cloud activity-history sending ended with KB5034204 on 2024-01-23.

Sources: [activity-history](https://support.microsoft.com/en-us/windows/privacy/windows-activity-history-and-your-privacy); [Per-user services](https://learn.microsoft.com/en-us/windows/application-management/per-user-services-in-windows)

## F180: original PDF page 91 (printed 90)

Category: factual error

Original:

the primary collection bus feeding the entire DiagTrack telemetry pipeline

Replacement:

one source for DiagTrack's telemetry pipeline

Reason: The original analysis describes multiple telemetry sources and separates the boot autologger from the live listener.

Date and scope: BSI/ERNW report, copyright 2018, Windows 10 1607 LTSB.

Sources: [BSI/ERNW SiSyPHuS Work Package 4: Telemetry](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Cyber-Sicherheit/SiSyPHus/Workpackage4_Telemetry.pdf?__blob=publicationFile&v=1)

## F181: original PDF page 91 (printed 90)

Category: version-dependent behavior

Original:

Its registry entry configures it to run in buffering mode, meaning it holds events in memory rather than writing continuously to disk, and the DiagTrack service itself is responsible for periodically writing that buffered data out to %ProgramData% \Microsoft\Diagnosis\ETLLogs\AutoLogger\AutoLogger-Diagtrack-Listener.etl .

Replacement:

In BSI's Windows 10 1607 analysis, it wrote to %ProgramData%\Microsoft\Diagnosis\ETLLogs\AutoLogger\AutoLogger-Diagtrack-Listener.etl before DiagTrack read and removed the file. The live Diagtrack-Listener session delivered events in real time. Logging mode depends on configuration and build.

Reason: The manuscript conflates memory buffering, real-time delivery, and boot-file logging; the correction states the original study scope.

Date and scope: BSI/ERNW 2018 report, sections 2.2 and 2.2.1, Windows 10 1607 LTSB; ETW logging-mode contract predates June 2026.

Sources: [BSI/ERNW SiSyPHuS Work Package 4: Telemetry](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Cyber-Sicherheit/SiSyPHus/Workpackage4_Telemetry.pdf?__blob=publicationFile&v=1); [Logging Mode Constants - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/logging-mode-constants)

## F182: original PDF page 91 (printed 90)

Category: version-dependent behavior

Original:

This one session alone subscribes to more than two hundred separate providers

Replacement:

The number and choice of providers vary with build, diagnostic-data level, and system state

Reason: BSI measured 9/93/105/112 autologger providers at different levels and explicitly warned that counts are dynamic. No unsupported universal count is selected.

Date and scope: BSI/ERNW 2018 report, Table 3, Windows 10 1607 LTSB.

Sources: [BSI/ERNW SiSyPHuS Work Package 4: Telemetry](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Cyber-Sicherheit/SiSyPHus/Workpackage4_Telemetry.pdf?__blob=publicationFile&v=1)

## F183: original PDF page 91 (printed 90)

Category: version-dependent behavior

Original:

(subscribed at essentially full verbosity)

Replacement:

(with verbosity set by configuration)

Reason: A provider name does not establish its level/keyword subscription; avoid claiming full collection without a configuration sample.

Date and scope: AutoLogger EnableLevel/MatchAnyKeyword/MatchAllKeyword documented for Vista and later; immutable Microsoft source frozen June 2026.

Sources: [Configuring and Starting an AutoLogger Session - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/configuring-and-starting-an-autologger-session); [EVENT_DESCRIPTOR (evntprov.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/evntprov/ns-evntprov-event_descriptor)

## F184: original PDF page 92 (printed 91)

Category: version-dependent behavior

Original:

typically sized around two to four megabytes

Replacement:

with its size set by configuration

Reason: Microsoft documents configurable buffer counts and sizes; its debugger example has four 4096-byte CKCL buffers, so 2–4 MB is not a portable default.

Date and scope: Microsoft SystemCollector documentation dated 2022-08-17; indirect-display debugging example documented before the cutoff.

Sources: [SystemCollector](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/systemcollector); [Debugging Indirect Display Drivers - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/indirect-display-debugging)

## F185: original PDF page 92 (printed 91)

Category: factual error

Original:

holds live ETL files that

Replacement:

holds ETW backing files that

Reason: Real-time backing files are not a universal shadow copy of circular memory sessions.

Date and scope: Microsoft ETW overview text preserved at immutable pre-cutoff June 2026 source.

Sources: [About Event Tracing - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/about-event-tracing)

## F186: original PDF page 93 (printed 92)

Category: factual error

Original:

shadow the in-memory circular buffers of several of the sessions above, written by the ETW subsystem independently of each session's own file configuration. You'll typically find backups here for the DiagTrack listener, DiagLog, and, most importantly for investigative purposes, the Application, System, and Security event log sessions, with the security backup in particular flagged as critical, since it can contain raw ETW event records from before an attacker cleared Security.evtx , or events that simply hadn't yet been formatted into the EVTX file at all.

Replacement:

support real-time sessions when consumers are absent or fall behind. Their presence and contents depend on the active sessions and system state. Files associated with event-log sessions may offer extra evidence, but they are not a guaranteed archive of events erased from Security.evtx. Check what survives on the system rather than assuming every circular buffer has a disk copy.

Reason: ETW distinguishes buffering-only mode from real-time backing files. The original guarantees backing for unrelated sessions and overstates forensic persistence.

Date and scope: Microsoft logging-mode and missing-events documentation predates July 2026, verified in its June 2026 immutable source.

Sources: [About Event Tracing - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/about-event-tracing); [Logging Mode Constants - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/logging-mode-constants)

## F187: original PDF page 94 (printed 93)

Category: factual error

Original:

each with the full path, process ID, and byte count involved

Replacement:

with fields that vary by event; file identifiers may need matching to name events

Reason: Read/write events carry file identifiers and I/O sizes; Microsoft instructs consumers to match identifiers to name events. A full path is not present in every event.

Date and scope: Microsoft FileIo_ReadWrite documentation dated 2018-05-31, last updated 2021-01-07.

Sources: [FileIo_ReadWrite class - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/fileio-readwrite)

## F188: original PDF page 95 (printed 94)

Category: factual error

Original:

Registry activity is covered by a single provider

Replacement:

Registry activity is covered in detail by the provider

Reason: Kernel-Registry is not the only provider that can report registry activity. The following event-provider list must not claim exclusivity.

Date and scope: Kernel registry tracing predates Vista; Windows Security auditing also has registry events before the cutoff.

Sources: [Registry class - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/etw/registry); [4657(S) A registry value was modified. - Windows 10](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4657)

## F189: original PDF page 85 (printed 84)

Category: factual error

Original:

fires whenever an executable image (an EXE, DLL, or driver) gets mapped into a process, including into kernel space itself when the process ID passed is zero.

Replacement:

fires when executable images are mapped into a process or kernel space (reported with process ID zero). SEC_IMAGE_NO_EXECUTE mappings are excluded.

Reason: Microsoft explicitly excludes images mapped with SEC_IMAGE_NO_EXECUTE from load-image notifications.

Date and scope: Windows driver callback documentation, immutable snapshot 2026-05-29; original API available Windows 2000 and later.

Sources: [PLOAD_IMAGE_NOTIFY_ROUTINE (ntddk.h) - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine)

## F190: original PDF page 6 (printed 5)

Category: factual error

Original:

a second, less well-known hive called UsrClass.dat sitting alongside it

Replacement:

a second hive, UsrClass.dat, under %LocalAppData%\Microsoft\Windows

Reason: UsrClass.dat is not next to NTUSER.DAT in the profile root; it is in Local AppData.

Date and scope: Microsoft KB3048895 describes this path in a Windows profile issue introduced by the 2015-01-13 update.

Sources: [Profile loading fails - Windows Server](https://learn.microsoft.com/en-us/troubleshoot/windows-server/user-profiles-and-logon/desktop-location-unavailable)

## F191: original PDF page 163 (printed 162)

Category: factual error

Original:

This concludes the book's coverage of the source research. Every service, registry key, file path, database schema, and technique documented across the three reference documents behind this project appears somewhere in the preceding forty-four chapters.

Replacement:

References
These sources were consulted for the technical accuracy review. Windows developments introduced after June 2026 are outside this book's scope. Studies of particular builds should be read within that scope. The companion change log records the exact passages, historical source versions, and unresolved questions.

Reason: Replace the unauditable claim about three unnamed research documents with the actual audit references, as the author requested.

Date and scope: Author instruction 2026-10-15; this is a provenance correction, not a new Windows development.

## F192: original PDF page 54 (printed 53)

Category: factual error

Original:

a running log of every change made to the file system: creates, deletes, renames, data extensions, and security changes, each captured as its own record

Replacement:

a running log of file-system changes: creates, deletes, renames, data extensions, and security changes. Repeated changes can share accumulated reason flags

Reason: USN records accumulate reason flags between file opens/closes; they do not provide a one-record-per-operation history.

Date and scope: Microsoft change-journal record contract documented before June 2026; immutable source snapshot 2026-06-18.

Sources: [Change Journal Records - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/fileio/change-journal-records)

## F193: original PDF page 55 (printed 54)

Category: factual error

Original:

found at the root of the system drive

Replacement:

found at the root of each participating volume

Reason: Recycle Bin content is per volume, not limited to the Windows system drive.

Date and scope: Dissect original parser frozen at 2026-06-10 checks the roots of available volumes.

Sources: [fox-it-dissect.target--dissect__target__plugins__os__windows__recyclebin.py](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/recyclebin.py)

## F194: original PDF page 58 (printed 57)

Category: factual error

Original:

Every Windows Event Log lives as a .evtx file under

Replacement:

By default, Windows Event Logs use .evtx files under

Reason: A channel may have a configured log-file path; the default directory is not mandatory.

Date and scope: EvtChannelLoggingConfigLogFilePath documented since Vista/Server 2008; Microsoft enum documentation 2022-01-30.

Sources: [EVT_CHANNEL_CONFIG_PROPERTY_ID (winevt.h) - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winevt/ne-winevt-evt_channel_config_property_id)

## F195: original PDF page 61 (printed 60)

Category: version-dependent behavior

Original:

For ordinary user-mode application crashes, that queue sits at

Replacement:

Per-user queues can be found at

Reason: LocalAppData and ProgramData report stores must not be assigned solely from whether a crashing app is elevated.

Date and scope: Microsoft WER settings documentation 2022-05-17; Microsoft report-location example published before June 2026.

Sources: [WER Settings - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/wer/wer-settings); [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-wer-reports)

## F196: original PDF page 61 (printed 60)

Category: factual error

Original:

Crashes in elevated processes generate the SYSTEM-context equivalent under

Replacement:

System-wide reports use the parallel store under

Reason: ProgramData is a system-wide WER store, not exclusively an elevated-process crash directory.

Date and scope: Microsoft WER report-location example; immutable Windows Server documentation snapshot 2026-06-30.

Sources: [Troubleshooting a Failover Cluster using Windows Error Reporting](https://learn.microsoft.com/en-us/windows-server/failover-clustering/troubleshooting-using-wer-reports)

## F197: original PDF page 62 (printed 61)

Category: factual error

Original:

a kernel crash that didn't produce a full system dump

Replacement:

a live kernel dump taken while Windows can continue running

Reason: A live kernel dump need not be a system crash.

Date and scope: Kernel live dump architecture documented in the Microsoft source preserved at 2026-06-30.

Sources: [Kernel Live Dump Code Reference - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/kernel-live-dump-code-reference)

## F198: original PDF page 63 (printed 62)

Category: factual error

Original:

an "automatic" mode that adapts based on available disk space

Replacement:

an "automatic" kernel-dump mode that lets Windows adjust paging-file size

Reason: Automatic Memory Dump contains kernel-dump information and changes paging-file management, not a generic choice based on free disk space.

Date and scope: Microsoft Automatic Memory Dump documentation dated 2018-05-08, last updated 2025-07-18.

Sources: [Automatic Memory Dump - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/automatic-memory-dump)

## F199: original PDF page 63 (printed 62)

Category: factual error

Original:

Its header

Replacement:

The user-mode header

Reason: Keep the header description attached to the user-mode MINIDUMP format after F071 distinguishes kernel dump formats.

Date and scope: User-mode and kernel dump formats predate June 2026; Microsoft driver dump-format documentation is pinned before the cutoff.

Sources: [Varieties of Kernel-Mode Dump Files - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/varieties-of-kernel-mode-dump-files)

## F200: original PDF page 64 (printed 63)

Category: factual error

Original:

to the Microsoft-Windows-Windows Error Reporting/Operational channel (event ID 1001 for a recorded fault bucket, 1002 for a hang report) and to Application.evtx itself

Replacement:

through Microsoft-Windows-WER-Diag and in Application.evtx

Reason: The analyzed Microsoft WER-Diag manifest has events 1–5, not Application-log events 1001/1002. Correct the provider reference without inventing replacement operational-channel IDs.

Date and scope: Microsoft Windows 10 build 17134 manifest, original extraction preserved in repository commit 2020-03-28.

Sources: [wer-diag-manifest](https://github.com/repnz/etw-providers-docs/blob/d5f68e8acda5da154ab44e405b610dd8c2ba1164/Manifests-Win10-17134/Microsoft-Windows-WER-Diag.xml)

## F201: original PDF page 71 (printed 70)

Category: factual error

Original:

the complete text content of the file itself

Replacement:

searchable text extracted from the file

Reason: The search index is filtered/indexed content and should not be promised as a complete stored copy of every document.

Date and scope: Dissect original Windows Search parser at 2026-06-10; format specifications document ESE property-store layouts by 2021.

Sources: [search-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/search.py)

## F202: original PDF page 71 (printed 70)

Category: version-dependent behavior

Original:

Inside the database, a table called SystemIndex_0A holds the actual full-text inverted index (the structure that makes searching fast), SystemIndex_Gthr tracks the crawl queue and its current state, and MSysObjects is ESENT's own internal catalog table.

Replacement:

ESE versions use property tables such as SystemIndex_0A or SystemIndex_PropertyStore, gathering tables such as SystemIndex_Gthr, and the MSysObjects catalog. SQLite versions use SystemIndex_1_PropertyStore and its metadata table.

Reason: SystemIndex_0A is an older item/property table, not a portable name for the full-text inverted index; modern ESE and SQLite layouts differ.

Date and scope: libyal original format research frozen at 2021-06-05; Dissect SQLite/ESE implementation frozen at 2026-06-10.

Sources: [search-spec](https://github.com/libyal/esedb-kb/blob/7308a338353a7c416b58207853bedc45289a1b7c/documentation/Windows%20Search.asciidoc); [search-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/search.py)

## F203: original PDF page 76 (printed 75)

Category: factual error

Original:

a Cookies database and its newer network-partitioned sibling under Network\Cookies

Replacement:

a Cookies database, found under Network\Cookies on newer builds

Reason: Network/Cookies is a profile storage location, not evidence of a separate database type or partitioning scheme.

Date and scope: Dissect original Chromium profile parser frozen at 2026-06-10.

Sources: [chromium-profile-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/apps/browser/chromium.py)

## F204: original PDF page 40 (printed 39)

Category: factual error

Original:

because the embedded shell item encodes a full path

Replacement:

where shell items or related artifacts provide a path

Reason: RecentDocs filename and shell-item data must not be assumed to contain a complete absolute path in every entry.

Date and scope: Dissect original MRU parser, immutable source dated 2026-06-10.

Sources: [mru-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/regf/mru.py)

## F205: original PDF page 41 (printed 40)

Category: factual error

Original:

And two keys, TypedURLs under the modern Explorer path and its older counterpart directly under HKCU\Software\Microsoft\Internet

Replacement:

And Internet Explorer's TypedURLs key under HKCU\Software\Microsoft\Internet

Reason: Correct the verified Internet Explorer TypedURLs branch; no source supports a universal modern Explorer TypedURLs location.

Date and scope: Original RegRipper parser, immutable repository commit dated 2026-05-27.

Sources: [typedurls-parser](https://github.com/keydet89/RegRipper3.0/blob/ec96dd4a6a5c3ea70d8fece9b47a374f83582335/plugins/typedurls.pl)

## F206: original PDF page 42 (printed 41)

Category: factual error

Original:

Explorer\TypedURLs , preserve URLs typed into Internet Explorer or legacy Edge.

Replacement:

Explorer\TypedURLs preserves URLs typed into Internet Explorer; legacy Edge uses separate browser artifacts.

Reason: Continue the corrected TypedURLs location and scope over the page break.

Date and scope: Original RegRipper parser, immutable repository commit dated 2026-05-27.

Sources: [typedurls-parser](https://github.com/keydet89/RegRipper3.0/blob/ec96dd4a6a5c3ea70d8fece9b47a374f83582335/plugins/typedurls.pl)

## F207: original PDF page 102 (printed 101)

Category: factual error

Original:

the definitive source for whether a task is currently enabled and when it last actually ran

Replacement:

one source for whether a task is enabled and when it last ran

Reason: TaskCache is a forensic source that can be manipulated or disagree with runtime state, not a definitive authority by itself.

Date and scope: G DATA original Windows 10 1909 research, 2022-06-01.

Sources: [tasks-research](https://cyber.wtf/2022/06/01/windows-registry-analysis-todays-episode-tasks/)

## F208: original PDF page 103 (printed 102)

Category: factual error

Original:

Every meaningful lifecycle event for a task also gets logged to

Replacement:

When enabled, the task history channel can record lifecycle events in

Reason: Task history is configurable; events must not be guaranteed without the channel being enabled and retained.

Date and scope: Task Scheduler 2.0 documentation for Vista and later; original TaskEvent implementation snapshot 2020-02-29.

Sources: [Task Scheduler for developers - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page); [task-events](https://github.com/dahall/TaskScheduler/blob/cce3ff7a1613d3d487ab8835711dfcb3480fadae/TaskService/TaskEvent.cs)

## F209: original PDF page 30 (printed 29)

Category: factual error

Original:

srum.dll

Replacement:

srumsvc.dll

Reason: The Microsoft-signed SRUM service module is named srumsvc.dll; srum.dll is not the module identified in the source.

Date and scope: Original extraction of Microsoft Windows 10 2004 binary version 10.0.19041.207 (2020); Windows 8 integration with DPS documented by Khatri in 2015.

Sources: [srumsvc.dll | System Resource Usage Monitor Service](https://strontic.github.io/xcyclopedia/library/srumsvc.dll-1160C033FC004C1FA71D5EBD14586FAF.html); [Yogesh Khatri: Forensic implications of System Resource Usage Monitor (SRUM) data in Windows 8](https://www.sciencedirect.com/science/article/pii/S1742287615000031)

## F210: original PDF page 79 (printed 78)

Category: factual error

Original:

Every toast, badge, and tile notification that's crossed a Windows PC gets recorded, at least temporarily, in

Replacement:

Windows can retain toast, badge, and tile notifications temporarily in

Reason: The database has retention limits and is not a guaranteed complete record of every notification.

Date and scope: Domingues, Andrade, Frade, published 2022-01-31; tests on Windows 10 1909 and Windows 11 21H2, Tables 3–7.

Sources: [Domingues, Andrade, Frade: A Digital Forensic View of Windows 10 Notifications](https://pdfs.semanticscholar.org/23d3/ca2eb05b56bd13e8fafe5ddc898cd18c90b9.pdf); [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F211: original PDF page 79 (printed 78)

Category: factual error

Original:

a type (toast, badge, tile, or raw)

Replacement:

a type such as toast, badge, tile, or toastCondensed

Reason: The studied Notification table uses these graphical notification types; raw notifications are not the listed table value.

Date and scope: Domingues, Andrade, Frade, published 2022-01-31; tests on Windows 10 1909 and Windows 11 21H2, Tables 3–7.

Sources: [Domingues, Andrade, Frade: A Digital Forensic View of Windows 10 Notifications](https://pdfs.semanticscholar.org/23d3/ca2eb05b56bd13e8fafe5ddc898cd18c90b9.pdf); [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F212: original PDF page 79 (printed 78)

Category: factual error

Original:

when it was created, when it was completed or dismissed, and when it was set to expire

Replacement:

when it arrived and when it was set to expire

Reason: The published schema has ArrivalTime and ExpiryTime, not direct user-read or dismissal timestamps.

Date and scope: Domingues, Andrade, Frade, published 2022-01-31; tests on Windows 10 1909 and Windows 11 21H2, Tables 3–7.

Sources: [Domingues, Andrade, Frade: A Digital Forensic View of Windows 10 Notifications](https://pdfs.semanticscholar.org/23d3/ca2eb05b56bd13e8fafe5ddc898cd18c90b9.pdf); [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F213: original PDF page 79 (printed 78)

Category: factual error

Original:

A companion NotificationHandler table maps each registered app to its AUMID, records the WNS channel URI it was assigned, and tracks when that registration was created and last modified.

Replacement:

NotificationHandler maps handler IDs to app identities and records registration times; WNSPushChannel holds channel details.

Reason: Channel details have a separate WNSPushChannel table; do not assign all its fields to NotificationHandler.

Date and scope: Domingues, Andrade, Frade, published 2022-01-31; tests on Windows 10 1909 and Windows 11 21H2, Tables 3–7.

Sources: [Domingues, Andrade, Frade: A Digital Forensic View of Windows 10 Notifications](https://pdfs.semanticscholar.org/23d3/ca2eb05b56bd13e8fafe5ddc898cd18c90b9.pdf); [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F214: original PDF page 22 (printed 21)

Category: factual error

Original:

transmits file metadata over HTTPS

Replacement:

transfers files and metadata over HTTP or HTTPS

Reason: The Windows WebDAV redirector supports HTTP as well as HTTPS. The original wording presents HTTPS as the only transport.

Date and scope: Microsoft's WebDAV Redirector article is dated 2014-03-28 and was last updated before the cutoff, on 2025-12-20. Its examples use HTTP; its authentication settings distinguish SSL-protected connections. This is an existing behavior, not a post-June 2026 development.

Sources: [Using the WebDAV Redirector](https://learn.microsoft.com/en-us/iis/publish/using-webdav/using-the-webdav-redirector)

## F215: original PDF page 55 (printed 54)

Category: factual error

Original:

Live systems can be queried directly with fsutil usn readjournal , though a complete extraction generally requires raw volume access instead.

Replacement:

Live systems can be queried with fsutil usn readjournal or the documented journal API to read retained records.

Reason: The documented control code reads retained journal records between USN values through a volume handle. Raw filesystem extraction is a separate acquisition choice, not a general requirement for reading all retained records. This correction makes no recovery promise about older data outside the live journal.

Date and scope: Microsoft FSCTL_READ_USN_JOURNAL documentation dated 2018-12-05, with Windows XP as its minimum supported client; the checked source is pinned to the 2026-06-29 MicrosoftDocs/sdk-api commit.

Sources: [FSCTL_READ_USN_JOURNAL - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winioctl/ni-winioctl-fsctl_read_usn_journal); [FSCTL_QUERY_USN_JOURNAL - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/api/winioctl/ni-winioctl-fsctl_query_usn_journal); [Change Journal Records - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/fileio/change-journal-records)

## F216: original PDF page 74 (printed 73)

Category: factual error

Original:

The StartTime and EndTime columns together describe a genuine window of use for a given file or application, rather than a single access moment.

Replacement:

The StartTime and EndTime columns describe an activity interval recorded through the app; they do not prove continuous use by a person.

Reason: Applications create and dispose UserActivity sessions. The stored interval therefore depends on the application's reporting and does not independently establish uninterrupted human interaction.

Date and scope: Microsoft's User Activities documentation is dated 2021-05-05, last updated 2025-06-10, and identifies Timeline integration with Windows 10 build 1803. The accompanying original WindowsTimeline research is pinned to 2023-02-16.

Sources: [Continue user activity, even across devices - UWP applications](https://learn.microsoft.com/en-us/windows/uwp/launch-resume/useractivities); [timeline-parser](https://github.com/kacos2000/WindowsTimeline/blob/696293696cc5d6ed6b5c82cb61139883b6a6505b/README.md)

## F217: original PDF page 147 (printed 146)

Category: factual error

Original:

records the display name, version, publisher, install date, install location, an uninstall command string, and an estimated installed size

Replacement:

records the display name, version, publisher, installation date (which patches or repairs can change), install location, an uninstall command string, and an estimated installed size

Reason: For an MSI product, InstallDate can be replaced when a patch is applied or removed or a qualifying repair runs. It records the original installation date only when the product has not been serviced in those ways.

Date and scope: Microsoft's Windows Installer Uninstall Registry Key documentation is dated 2018-05-31. The exact checked text is present in the immutable MicrosoftDocs/win32 source snapshot of 2026-06-18.

Sources: [Windows Installer Properties for the Uninstall Registry Key - Win32 apps](https://learn.microsoft.com/en-us/windows/win32/msi/uninstall-registry-key)

## F218: original PDF page 14 (printed 13)

Category: verified factual correction

Original:

dmwappushsvc , the WAP Push Message Routing Service

Replacement:

dmwappushservice, the WAP Push Message Routing Service

Reason: Corrects the service name, retaining the surrounding prose and claims.

Date and scope: Microsoft service guidance in the immutable 25 June 2026 snapshot names dmwappushservice. Read-only metadata on this Windows 11 25H2 host corroborates it. This is a documented-by date, not an introduction date.

Sources: [Guidance on configuring system services - Windows IoT Enterprise](https://learn.microsoft.com/en-us/windows/iot/iot-enterprise/optimize/services)

## F219: original PDF page 18 (printed 17)

Category: verified factual correction

Original:

Two more services, SensrSvc and SensorMonitorSvc , route sensor API calls and record things like automatic brightness adjustments and activity detection, respectively.

Replacement:

Two more services, SensrSvc and SensorService, support automatic brightness adjustments and sensor functions including orientation and history, respectively.

Reason: Corrects the nonexistent service name and the two documented sensor-service roles, keeping the same sentence and technical scope.

Date and scope: Microsoft service guidance, source snapshot 25 June 2026, distinguishes Sensor Monitoring Service (SensrSvc) and Sensor Service (SensorService). Host service metadata corroborates these names.

Sources: [Guidance on configuring system services - Windows IoT Enterprise](https://learn.microsoft.com/en-us/windows/iot/iot-enterprise/optimize/services)

## F220: original PDF page 22 (printed 21)

Category: verified factual correction

Original:

and keeps its own most-recently-used list under the Explorer "Map Network Drive MRU" key

Replacement:

while Explorer keeps mapped paths under its "Map Network Drive MRU" key

Reason: Attributes the shell MRU to Explorer rather than to the WebClient service.

Date and scope: Microsoft WebDAV documentation and the pre-cutoff Dissect MRU parser establish the distinct mechanisms. Dissect source was pinned on 10 June 2026.

Sources: [Using the WebDAV Redirector](https://learn.microsoft.com/en-us/iis/publish/using-webdav/using-the-webdav-redirector); [mru-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/regf/mru.py)

## F221: original PDF page 65 (printed 64)

Category: verified factual correction

Original:

producing a ZIP archive at a path the user chooses at runtime, named PSR_recording_{date}_{time}.zip

Replacement:

producing a ZIP archive at a path and with a filename the user chooses

Reason: Corrects the fixed archive-filename claim without changing the explanation.

Date and scope: The original Windows 7 PSR study was published 12 February 2009 and last modified 29 July 2025; it explicitly describes choosing the output filename.

Sources: [Windows 7 Cool Feature - Problem Steps Recorder - Petri IT Knowledgebase](https://petri.com/windows-7-cool-feature-problem-steps-recorder/)

## F222: original PDF page 65 (printed 64)

Category: verified factual correction

Original:

and a companion recording.xml file lists the actual event timeline

Replacement:

and XML embedded in the MHTML report lists the actual event timeline

Reason: Corrects the location of the XML within the report.

Date and scope: Daniel Petri's original PSR study, 12 February 2009, describes the compiled MHTML report and its embedded XML. Its linked sample returned HTTP 403, so no sample execution is claimed.

Sources: [Windows 7 Cool Feature - Problem Steps Recorder - Petri IT Knowledgebase](https://petri.com/windows-7-cool-feature-problem-steps-recorder/)

## F223: original PDF page 84 (printed 83)

Category: verified factual correction

Original:

WdFilter.sys , registered at filter altitude 328010

Replacement:

WdFilter.sys, also a filesystem minifilter at altitude 328010

Reason: Distinguishes filesystem filter altitude from process-notification registration. All surrounding callback discussion is retained.

Date and scope: Microsoft's allocated altitudes and minifilter documentation are preserved in pre-30 June 2026 source snapshots.

Sources: [Allocated Filter Altitudes - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ifs/allocated-altitudes); [Load Order Groups and Altitudes for Minifilter Drivers - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)

## F224: original PDF page 85 (printed 84)

Category: verified factual correction

Original:

whether it's a shared section mapped into every process

Replacement:

ImageMappedToAllPids (documented as always zero)

Reason: Corrects the documented IMAGE_INFO field meaning without narrowing the rest of the callback explanation.

Date and scope: Microsoft IMAGE_INFO documentation dated 10 January 2023 explicitly says ImageMappedToAllPids is always zero; checked at immutable source snapshot 29 May 2026.

Sources: [_IMAGE_INFO (ntddk.h) - Windows drivers](https://learn.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_image_info)

## F225: original PDF page 107 (printed 106)

Category: verified factual correction

Original:

locally under %SystemRoot%\System32\LogFiles\dosvc\

Replacement:

in local ETL logs readable with Get-DeliveryOptimizationLog

Reason: Replaces the wrong log path with the documented reader while retaining the stated logged evidence.

Date and scope: Microsoft Monitor Delivery Optimization, dated 20 May 2026, documents Get-DeliveryOptimizationLog from Windows 10 version 1803 onward. The command reference is pinned at 24 June 2026. The local NetworkService log directory was corroborated without running the service.

Sources: [Monitor Delivery Optimization](https://learn.microsoft.com/en-us/windows/deployment/do/waas-delivery-optimization-monitor); [Get-DeliveryOptimizationLog (DeliveryOptimization)](https://learn.microsoft.com/en-us/powershell/module/deliveryoptimization/get-deliveryoptimizationlog)

## F226: original PDF page 108 (printed 107)

Category: verified factual correction

Original:

The Microsoft Account Token Service

Replacement:

The Microsoft Account Sign-in Assistant

Reason: Uses the official name of wlidsvc.

Date and scope: Microsoft service descriptions in the 30 June 2026 immutable snapshot identify the Microsoft Account Sign-in Assistant.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server)

## F227: original PDF page 108 (printed 107)

Category: verified factual correction

Original:

and, for organizational accounts, login.microsoftonline.com

Replacement:

; organizational sign-in uses separate identity components and login.microsoftonline.com

Reason: Corrects the attribution of organizational identity sign-in to the consumer Microsoft-account service.

Date and scope: Microsoft service and Windows connection documentation checked at pre-cutoff snapshots; the connection guidance was dated 12 February 2026.

Sources: [Security guidelines for system services in Windows Server 2016](https://learn.microsoft.com/en-us/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server); [Manage connections from Windows 10 and Windows 11 Server/Enterprise editions operating system components to Microsoft services - Windows Privacy](https://learn.microsoft.com/en-us/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)

## F228: original PDF page 113 (printed 112)

Category: verified factual correction

Original:

the delivery mechanism behind every toast and background notification a Windows app can receive

Replacement:

the delivery mechanism for cloud-sent toast and background notifications

Reason: Apps can also generate local notifications; those are not all cloud WNS deliveries.

Date and scope: Microsoft WNS overview and per-user notification service documentation are pinned before 30 June 2026. The August 2026 live-page update is not used.

Sources: [Windows Push Notification Services (WNS) overview - Windows apps](https://learn.microsoft.com/en-us/windows/apps/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview); [Per-user services](https://learn.microsoft.com/en-us/windows/application-management/per-user-services-in-windows)

## F229: original PDF page 113 (printed 112)

Category: verified factual correction

Original:

a per-device channel token that's renewed roughly every thirty days and is used by cloud apps to target notifications at this specific device

Replacement:

an app-and-user-specific channel URI that expires after thirty days and is renewed for cloud notifications

Reason: Corrects the identity and expiry of the documented UWP WNS channel.

Date and scope: The immutable Microsoft WNS source of 25 June 2026 describes an app/user channel and thirty-day expiry. This is a documented-by date, not the date WNS was introduced.

Sources: [Windows Push Notification Services (WNS) overview - Windows apps](https://learn.microsoft.com/en-us/windows/apps/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)

## F230: original PDF page 113 (printed 112)

Category: verified factual correction

Original:

and the Handler table specifically is where an app's registered WNS channel URI ends up stored

Replacement:

and WNSPushChannel stores the channel URI, linked to the notification handler

Reason: Corrects the repeated channel URI table name.

Date and scope: Domingues, Andrade and Frade's original notification-database study was published 31 January 2022 (Windows 10 1909 and Windows 11 21H2). The read-only host SQLite schema corroborates WNSPushChannel; no notification rows were read.

Sources: [Domingues, Andrade, Frade: A Digital Forensic View of Windows 10 Notifications](https://pdfs.semanticscholar.org/23d3/ca2eb05b56bd13e8fafe5ddc898cd18c90b9.pdf); [notifications-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/notifications.py)

## F231: original PDF page 116 (printed 115)

Category: verified factual correction

Original:

while the encrypted XML alone is useless off that specific machine

Replacement:

while offline decryption requires the appropriate DPAPI system keys as well as the XML

Reason: Corrects the off-machine impossibility claim; the required keys, rather than physical location, determine offline decryption.

Date and scope: The Dissect DPAPI implementation pinned on 10 June 2026 implements offline key discovery and decryption. No credentials were accessed during the host checks.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py); [dpapi-masterkey](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/master_key.py)

## F232: original PDF page 117 (printed 116)

Category: verified factual correction

Original:

%AppData% \Microsoft\Vault\{VaultGUID}\

Replacement:

%LocalAppData%\Microsoft\Vault\{VaultGUID}\

Reason: Corrects the usual user Vault path from Roaming to Local AppData.

Date and scope: The pre-cutoff Dissect credential discovery implementation, pinned 10 June 2026, identifies LocalAppData Vault storage. Other stores and formats remain described in context.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py)

## F233: original PDF page 117 (printed 116)

Category: verified factual correction

Original:

Every credential file shares a common binary header

Replacement:

A legacy credential blob has a binary header

Reason: Distinguishes the described credential-blob header from the different Vault record/policy formats.

Date and scope: Pre-cutoff Dissect DPAPI format definitions, pinned 10 June 2026, distinguish the binary structures.

Sources: [dpapi-parser](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/dpapi.py); [dpapi-masterkey](https://github.com/fox-it/dissect.target/blob/76991b08a3afdacfccf4dd23597c940ce58b4988/dissect/target/plugins/os/windows/dpapi/master_key.py)

## F234: original PDF page 118 (printed 117)

Category: verified factual correction

Original:

Internet Explorer and legacy Edge stored autofill form passwords

Replacement:

older Internet Explorer versions stored autofill form passwords

Reason: Corrects the attribution of the older Storage2 mechanism to legacy Edge.

Date and scope: The original DPAPI research and pre-cutoff implementations distinguish IE Storage2 from later Vault/browser credential storage. See the dated source catalog.

Sources: [Offensive DPAPI With Nemesis](https://specterops.io/blog/2026/03/04/offensive-dpapi-with-nemesis/)
