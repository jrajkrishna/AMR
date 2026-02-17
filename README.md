# 📱 Service Reminder App

An Android app to store customer service records and receive automatic 5-month reminder notifications.

---

## ✨ Features
- ➕ Add customers with **Name**, **Mobile Number**, and **Service Date**
- 📋 View all customers in a clean list with reminder dates
- ⏰ **Automatic notification** exactly **5 months** after service date
- ⚠️ Shows "Due" badge when a customer is overdue
- 🗑️ Delete customer + cancels their reminder
- 🔄 Reminders survive phone restarts (BootReceiver)

---

## 🛠 Setup Instructions

### Requirements
- Android Studio Hedgehog or newer
- Android SDK 26+
- Kotlin 1.9+

### Steps to Run

1. **Open Android Studio** → File → New → Import Project  
2. Select the `CustomerServiceApp` folder
3. Wait for Gradle sync to complete
4. Connect your Android device or start an emulator
5. Click ▶️ **Run**

---

## 📁 Project Structure

```
CustomerServiceApp/
├── app/
│   ├── build.gradle                  ← Dependencies
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/customerservice/
│       │   ├── Customer.kt           ← Room Entity (data model)
│       │   ├── CustomerDao.kt        ← Database queries
│       │   ├── CustomerDatabase.kt   ← Room database setup
│       │   ├── CustomerViewModel.kt  ← Business logic
│       │   ├── CustomerAdapter.kt    ← RecyclerView list
│       │   ├── MainActivity.kt       ← Customer list screen
│       │   ├── AddCustomerActivity.kt← Add customer screen
│       │   ├── ReminderWorker.kt     ← Notification sender
│       │   ├── ReminderScheduler.kt  ← Schedules 5-month delay
│       │   └── BootReceiver.kt       ← Reschedule on reboot
│       └── res/
│           ├── layout/
│           │   ├── activity_main.xml
│           │   ├── activity_add_customer.xml
│           │   └── item_customer.xml
│           ├── drawable/circle_bg.xml
│           └── values/themes.xml
```

---

## 📲 How It Works

1. You add a customer with their **service date**
2. App calculates `serviceDate + 5 months` as reminder time
3. **WorkManager** schedules a background job for that exact time
4. When the time arrives, a push notification is sent:
   > ⏰ **Service Due: [Customer Name]**  
   > 5 months since last service. Mobile: XXXXXXXXXX

5. Tapping the notification opens the app

---

## 🔔 Notification Permission
On Android 13+, the app will ask for notification permission on first launch. Please **Allow** it for reminders to work.

---

## 📦 Key Libraries Used
| Library | Purpose |
|---|---|
| Room | Local SQLite database |
| WorkManager | Reliable background task scheduling |
| LiveData + ViewModel | Reactive UI updates |
| Material Components | Beautiful UI design |
