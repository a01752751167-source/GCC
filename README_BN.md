# Teachers Attendance Android App — APK তৈরি (Android Studio ছাড়াই)

এই প্রজেক্টে HTML অ্যাপটি Android WebView-এ চালানোর জন্য রাখা হয়েছে। GitHub Actions ব্যবহার করে অনলাইনে APK বানানো যাবে; নিজের কম্পিউটারে Android Studio লাগবে না।

## সহজ পদ্ধতি: GitHub থেকে অনলাইনে APK তৈরি

### ১) GitHub-এ নতুন repository তৈরি করুন
1. https://github.com/new খুলুন এবং GitHub-এ সাইন ইন করুন।
2. Repository name দিন `teachers-attendance-android`।
3. **Private** নির্বাচন করুন (প্রস্তাবিত), তারপর **Create repository** চাপুন।

### ২) প্রজেক্ট ফাইল আপলোড করুন
1. এই ZIP ফাইলটি কম্পিউটারে Extract করুন।
2. নতুন GitHub repository-তে **Add file → Upload files** চাপুন।
3. Extract করা `TeachersAttendanceAndroid` ফোল্ডারের *ভেতরের সব ফাইল ও ফোল্ডার* নির্বাচন করে আপলোড করুন। `.github` ফোল্ডারটিও আপলোড হচ্ছে নিশ্চিত করুন—এর ভেতরে `workflows/build-apk.yml` আছে।
4. নিচে **Commit changes** চাপুন।

### ৩) Build শুরু/দেখুন
1. Repository-তে **Actions** ট্যাব খুলুন।
2. `Build Teachers Attendance APK` workflow দেখা উচিত। যদি না দেখা যায়, `main` branch-এ `.github/workflows/build-apk.yml` ফাইলটি আপলোড হয়েছে কি না দেখুন।
3. সর্বশেষ run খুলুন এবং সব ধাপ সবুজ টিক হওয়া পর্যন্ত অপেক্ষা করুন। প্রথম build-এ কয়েক মিনিট লাগতে পারে।

### ৪) APK ডাউনলোড করুন
1. সফল run-এর নিচে **Artifacts** অংশে `TeachersAttendance-debug-apk` চাপুন।
2. ডাউনলোড হওয়া ZIP Extract করুন। এর মধ্যে `app-debug.apk` থাকবে।
3. APK Android ফোনে পাঠিয়ে ইনস্টল করুন। ফোনে অনুমতি চাইলে কেবল নিজের তৈরি APK-এর জন্য অনুমতি দিন।

## যদি build ব্যর্থ হয়
- Actions run খুলে লাল চিহ্ন থাকা ধাপের error দেখুন।
- নিশ্চিত করুন সব ফাইল repository-র root-এ আছে—`app/`, `build.gradle.kts`, `settings.gradle.kts`, `.github/`। পুরো প্রজেক্ট একটি অতিরিক্ত nested folder-এর ভেতরে থাকলে workflow ফাইল খুঁজে নাও পেতে পারে।
- Error log-এর screenshot পাঠাতে পারেন; কোনো secret/API key প্রকাশ করবেন না।

## নিরাপত্তা ও সীমাবদ্ধতা
- এই পদ্ধতি debug APK বানায়; Play Store বা জনসাধারণের বিতরণের জন্য release signing আলাদা কাজ।
- Supabase `service_role` বা অন্য secret key HTML/APK-এ কখনো রাখবেন না। কেবল publishable/anon key ব্যবহার করুন এবং RLS ঠিক আছে নিশ্চিত করুন।
- APK তৈরির পর নিজের ফোনে লগইন, হাজিরা দেখা/সংরক্ষণ, রেট ও ব্যাকআপ পরীক্ষা করুন।
- GitHub repository private রাখুন। APK artifact ১৪ দিন পর্যন্ত থাকবে; পরে দরকার হলে পুনরায় build করতে হবে।
