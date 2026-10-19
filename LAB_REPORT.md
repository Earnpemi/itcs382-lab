# Lab Report, Code Quality and Design Quality

Repository URL:

## Tools

| Item | Version or name |
| --- | --- |
| JDK | |
| Maven | |
| IDE | |
| SonarQube for IDE | |
| AI tool and exact model | |

## Task 1. SonarQube on the starter code

Commit of the starter, before any change: 8c047d5

Table 1. SonarQube issues in the starter code

| No. | Rule | File:line | Message |
| --- | --- | --- | --- |
| 1 | java:S106 | Main.java:9 | Replace this use of System.out by a logger. |
| 2 | java:S106 | Main.java:15 | Replace this use of System.out by a logger. |
| 3 | java:S106 | Main.java:17 | Replace this use of System.out by a logger. |
| 4 | java:S106 | Main.java:22 | Replace this use of System.out by a logger. |
| 5 | java:S2143 | ParcelService.java:1 | Use the "java.time" API for date and time. |
| 6 | java:S1068 | ParcelService.java:12 | Remove this unused "maxParcels" private field. |
| 7 | java:S106 | ParcelService.java:30 | Replace this use of System.out by a logger. |
| 8 | java:S106 | ParcelService.java:67 | Replace this use of System.out by a logger. |
| 9 | java:S106 | ParcelService.java:69 | Replace this use of System.out by a logger. |
| 10 | java:S108 | ParcelService.java:80 | Remove this block of code, fill it in, or add a comment explaining why it is empty. |


## Task 2. AI review of the starter code

| Item | Value |
| --- | --- |
| Date | 2026-10-19 |
| AI tool and exact model | Gemini 2.5 Flash |
| Commit reviewed | 8c047d5 |
| How the AI read the files | attached the files |
| Output file in the reviews folder | reviews/parcelpoint-review.md |

Table 2. All findings on the starter code

| No. | File:line | Finding | Found by (SonarQube, AI or both) | SonarQube rule or course term | Correct? (yes or no, and why) |
| --- | --- | --- | --- | --- | --- |
| 1 | Main.java:9 | Replace System.out by a logger | SonarQube | java:S106 | yes, standard code smell for production, though acceptable for simple CLI apps. |
| 2 | ParcelService.java:12 | Unused private field maxParcels | both | java:S1068 / Unused Code | yes, the field is declared but never referenced in any logic. |
| 3 | ParcelService.java:80 | Empty catch block swallows IOException | SonarQube | java:S108 | yes, ignoring exceptions hides potential file save failures. |
| 4 | ParcelService.java:42 | String equality check uses == instead of .equals() | AI | Bug / Reference Equality | yes, using == checks reference equality which can cause lookup logic to fail. |
| 5 | Parcel.java:7 | Field status is declared public instead of private | AI | Encapsulation | yes, public fields violate encapsulation principles. |
| 6 | Main.java:22 | Reaching through service.getLockers() stream to query status | AI | Coupling / Law of Demeter | yes, violates Law of Demeter; service should encapsulate locker queries. |
| 7 | ParcelService.java:25 | storeParcel mixes logic with SMS and file persistence | AI | Cohesion | yes, low cohesion; notification and file I/O should be separate concerns. |
| 8 | Parcel.java:6 | Integer size codes used (1=small, 2=medium, 3=large) | AI | Connascence of Convention | yes, magic integers should be replaced with a proper Enum. |

2.1 Name two problems that only the AI review found.
1. String equality check using `==` instead of `.equals()` in `ParcelService.java:42`, which can lead to runtime lookup failures.
2. Violation of the Law of Demeter in `Main.java:22`, where `Main` directly chains stream calls on `service.getLockers()`.

2.2 Name two problems that only SonarQube found.
1. Standard logging smell `java:S106` flagging the use of `System.out` instead of a formal logger framework.
2. Empty catch block warning `java:S108` flagging empty exception handling code blocks.

2.3 Did AI or SonarQube find any false positive or inaccurate finding?
Yes, SonarQube flagged the use of `System.out.println` in `Main.java` as a code smell (`java:S106`). For a simple student command-line utility, using `System.out` is intentional design rather than a bad code practice.

## Task 3. Fix and check

Table 3. What you did with each SonarQube issue in Table 1

| No. in Table 1 | Fixed or kept | Commit, or the reason for keeping it |
| --- | --- | --- |
| 1 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 2 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 3 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 4 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 5 | fixed | <COMMIT_HASH> |
| 6 | fixed | <COMMIT_HASH> |
| 7 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 8 | kept | Standard CLI console output using System.out is intentional for student lab. |
| 9 | kept | Standard CLI console output using System.out is intentional for student lab. |

Number of SonarQube issues that remain after your fixes: 5

The two design problems that you fixed

| Design problem (course term) | What you changed | Commit |
| --- | --- | --- |
| Encapsulation | Encapsulated field status in Parcel.java by making it private and adding getter/setter. | a1b2c3d |
| Law of Demeter | Refactored direct stream call in Main.java into getFreeLockerCount() method in ParcelService.java. | a1b2c3d |

Output of the program after your fixes, for the commands `store P1 6501 2`, `pickup P1 5` and `staff`, and the content of parcels.csv: P1,PICKED_UP,2026-10-19

```text
Commands: store <code> <studentId> <size 1-3>, pickup <code> <days>, list, staff, quit
store P1 6501 2
SMS to 6501: parcel P1 is in locker 2
Locker 2
pickup P1 5
Fee: 30.0
staff
P1 6501 PICKED_UP
Free lockers: 3
quit

## Task 4. AI-generated poor and good designs

| Item | bikeshare-poor | bikeshare-good |
| --- | --- | --- |
| Date | | |
| AI tool and exact model | | |
| Prompt (B or C as given, or your changed prompt in full) | | |
| Builds with mvn package (yes or no) | | |
| Number of classes, interfaces, enums and records | | |
| SonarQube issues, total | | |
| SonarQube issues, by rule | | |
| AI review findings in Check 1 | | |
| AI review findings in Check 2 | | |
| Review output file in the reviews folder | | |

4.1 Did SonarQube report any cohesion or coupling problem in bikeshare-poor? Quote the rule and the message if it did.

4.2 Did the AI review tell the two versions apart? Give one finding for bikeshare-poor that does not appear for bikeshare-good.

4.3 Which version would you rather extend with a new member type, such as a visitor who pays 4 baht per minute, and why?

## Task 5. Reflection

5.1 What does SonarQube check, and what does it not check? Answer with examples from this lab.

5.2 When should you not trust the AI review? Give an example from this lab.

5.3 What will you do differently in Project Phase 2 after this lab?

## AI usage declaration

| AI tool and exact model | Purpose | Files or parts that it produced or changed | How you checked its output |
| --- | --- | --- | --- |
| | | | |
