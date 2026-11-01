# PaisaTrack Lite (Flutter / Android)

A simple offline loan and payment tracker. Data is stored in an on-device SQLite database.

## Build an Android APK

Requirements: Flutter stable (Dart 3.3+), Android SDK, Android build tools.

```bash
flutter pub get
flutter create . --platforms=android
flutter build apk --release
```

APK output: `build/app/outputs/flutter-apk/app-release.apk`

Install by transferring the APK to the Android phone and opening it. Android may ask to allow installation from that source.

## Included
- Borrower records (name, phone, notes)
- Multiple loans per borrower
- Adjustable interest (default 20%, including 0%)
- Daily / weekly / monthly schedule and editable agreed amount
- Quick payment entry for any positive amount
- Missed-payment entries
- Outstanding balance, due date, overdue and paid status
- Payment history
- Delete loan with explicit warning (also deletes its entries)
- JSON backup and restore
- Offline SQLite storage

## Important prototype notes
- Loan interest is simple one-time interest on principal: principal × rate. No additional interest is added after the due date.
- Weekly periods are rounded up to whole weeks; monthly periods are rounded up to 30-day periods. The final installment is implicitly adjusted to the remaining balance.
- A payment reduces the outstanding total by the full amount received. The app does not allocate interest vs principal separately.
- Missed payments are recorded as events and do not change the balance. This prototype does not generate a calendar of expected installments or automatically mark days missed.
- SQLite data survives app restarts and phone reboots, but can still be lost if app data is cleared, the app is uninstalled, or the phone is damaged. Use the backup feature regularly and store backup files somewhere separate from the phone.

## Android package setup
Run `flutter create . --platforms=android` from this directory to generate the standard Android Gradle wrapper and platform project for your installed Flutter version. Then build the APK as above.
