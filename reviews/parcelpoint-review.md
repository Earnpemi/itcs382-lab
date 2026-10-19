Files read: `Main.java`, `Parcel.java`, `ParcelService.java`, `Locker.java`

| No. | Check | Code location (file:line) | Finding | Severity | Suggested fix |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Check 1 | Main.java:7 | `Scanner` resource is never closed. | Should fix | Close `in` after the loop or use a try-with-resources statement. |
| 2 | Check 1 | ParcelService.java:5 | Unused imports `java.io.IOException` and `java.util.Date`. | Note | Remove unused import declarations. |
| 3 | Check 1 | ParcelService.java:12 | Unused field `maxParcels`. | Note | Remove the `maxParcels` field if it is not used. |
| 4 | Check 1 | ParcelService.java:42 | String equality check uses `==` instead of `.equals()`. | Must fix | Replace `parcel.getCode() == code` with `parcel.getCode().equals(code)`. |
| 5 | Check 1 | ParcelService.java:71 | Resource `FileWriter` is never explicitly closed. | Must fix | Wrap `FileWriter` in a try-with-resources statement or close it in a `finally` block. |
| 6 | Check 1 | ParcelService.java:75 | Empty catch block swallows `IOException`. | Should fix | Handle or log the caught `IOException` inside the catch block. |
| 7 | Check 2 | Parcel.java:7 | Field `status` is declared public instead of private. | Must fix | Change `status` modifier to `private` and add getter/setter methods. |
| 8 | Check 2 | ParcelService.java:21 | Returns internal collection `lockers` directly, allowing callers to modify state. | Must fix | Return an unmodifiable view or a copy of `lockers`. |
| 9 | Check 2 | ParcelService.java:25 | Weak cohesion: `storeParcel` mixes business logic with notification (SMS) and file persistence. | Should fix | Move notification and persistence calls out of `storeParcel` into separate dedicated components or methods. |
| 10 | Check 2 | ParcelService.java:51 | Feature envy: `fee()` performs calculations based entirely on attributes of `Parcel`. | Should fix | Move the `fee()` method logic into the `Parcel` class. |
| 11 | Check 2 | ParcelService.java:62 | Control coupling: `forStaff` boolean flag controls internal execution path and logic of `printParcels`. | Should fix | Split `printParcels` into two separate methods, one for customer view and one for staff view. |
| 12 | Check 2 | ParcelService.java:62 | Weak cohesion (logical): `printParcels` groups two distinct printing tasks based on a boolean parameter. | Should fix | Separate the staff printing and student printing concerns into distinct methods. |
| 13 | Check 2 | Main.java:22 | Reaching through `service.getLockers()` stream to query locker status shows tight coupling/LOD violation. | Should fix | Add a method `getFreeLockerCount()` in `ParcelService` to encapsulate locker query logic. |
| 14 | Check 2 | Parcel.java:6, Locker.java:5 | Connascence of convention / algorithm on integer sizes (1=small, 2=medium, 3=large). | Should fix | Replace integer size codes with a shared `Size` enum. |

### Number of findings for each check

* **Check 1:** 6 findings
* **Check 2:** 8 findings