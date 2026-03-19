# Xiaomi Gauguin-এ PostmarketOS ফ্ল্যাশ করার সম্পূর্ণ গাইড

## 📋 প্রয়োজনীয় জিনিস

- ADB (Android Debug Bridge)
- Fastboot
- USB কেবল (ডেটা ট্রান্সফার সমর্থনকারী)
- Windows/Linux/macOS কম্পিউটার
- ডাউনলোড করা `.img` ফাইল

## 🔧 টুলস ইনস্টলেশন

### Linux-এ:
```bash
sudo apt-get install android-tools-adb android-tools-fastboot
```

### Windows-এ:
- Google USB Driver ডাউনলোড করুন
- ADB/Fastboot টুলস সেটআপ করুন

### macOS-এ:
```bash
brew install android-platform-tools
```

## 📱 ধাপ ১: ডিভাইস প্রস্তুতি

### USB ডিবাগিং সক্ষম করুন:
1. Settings খুলুন
2. About Phone যান
3. Build Number ৭ বার ট্যাপ করুন (Developer Mode সক্ষম হবে)
4. Developer Options এ ফিরে যান
5. USB Debugging চেক করুন

## 🚀 ধাপ ২: Fastboot মোডে প্রবেশ করুন

```bash
# USB দিয়ে কম্পিউটারের সাথে সংযুক্ত করুন
adb devices  # যদি দেখা যায় তাহলে ঠিক আছে

# Fastboot মোডে রিবুট করুন
adb reboot bootloader

# নিশ্চিত করুন fastboot কাজ করছে
fastboot devices
```

## 💾 ধাপ ৩: IMG ফাইল ফ্ল্যাশ করুন

```bash
# পার্টিশন ওয়াইপ করুন (ঐচ্ছিক কিন্তু সুপারিশকৃত)
fastboot erase system
fastboot erase vendor
fastboot erase userdata

# IMG ফাইল ফ্ল্যাশ করুন
fastboot flash system pmos-xiaomi-gauguin-*.img

# রিবুট করুন
fastboot reboot
```

## ⏳ ধাপ ৪: প্রথম বুট অপেক্ষা করুন

- প্রথম বুট ৫-১০ মিনিট সময় নেবে
- ডিভাইস বেশ বার গুলি দেখাবে - এটি স্বাভাবিক
- ওয়াইফাই সংযোগ সেটআপ করুন

## ❌ ট্রাবলশুটিং

### সমস্যা: ADB ডিভাইস শনাক্ত করছে না

```bash
# ADB সার্ভার পুনরায় চালু করুন
adb kill-server
adb start-server

# Windows-এ USB ড্রাইভার পুনরায় ইনস্টল করুন
# Linux-এ udev rules যোগ করুন:
sudo usermod -aG plugdev $USER
```

### সমস্যা: Fastboot কাজ করছে না

```bash
# ফোন অফ করুন
# ভলিউম ডাউন + পাওয়ার বোতাম ধরে রাখুন
# Fastboot মোড প্রবেশ করুন (স্ক্রিনে দেখা যাবে)

# এবার চেষ্টা করুন:
fastboot devices
```

### সমস্যা: IMG ফাইল খুব বড়

```bash
# সংকুচিত IMG ব্যবহার করুন
fastboot flash system pmos-xiaomi-gauguin-*.img.xz
```

## 📞 সহায়তা এবং রেফারেন্স

- **PostmarketOS অফিসিয়াল**: https://postmarketos.org
- **Xiaomi Gauguin পোর্ট**: https://wiki.postmarketos.org/wiki/Xiaomi_Mi_10T_(xiaomi-gauguin)
- **GitHub Issues**: আপনার রিপোজিটরি Issues সেকশন
