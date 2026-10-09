DIGITAL CNC WOOD DESIGN HOUSE — Supabase + Netlify প্যাকেজ

এই ZIP-এ কী আছে
- index.html: Supabase থেকে ব্যবসার তথ্য ও গ্যালারি পড়ার জন্য ওয়েবসাইট
- admin.html: লগইন, ফোন/ঠিকানা সম্পাদনা, কাজের ছবি আপলোড/মোছার অ্যাডমিন প্যানেল
- supabase-setup.sql: ডেটাবেস টেবিল ও নিরাপত্তা নীতি তৈরির SQL
- netlify.toml: Netlify-তে প্রকাশের বেসিক সেটিং
- index-static-reference.html: আগের ডিজাইনের ওয়েবসাইটের রেফারেন্স কপি

সত্য অবস্থা:
এই প্যাকেজ এখনো প্রকাশিত নয়। আপনার Supabase Project URL এবং anon/publishable key যোগ করে SQL চালানো, Storage bucket বানানো, Authentication-এ নিজের অ্যাডমিন user তৈরি করা, সেই user-কে admin_users টেবিলে যুক্ত করা এবং Netlify-তে deploy করার পরেই লাইভ হবে। এসব ধাপ শেষ না হওয়া পর্যন্ত লাইভ ডেটাবেস/অ্যাডমিন কাজ করবে না।

সহজ সেটআপ
১. https://supabase.com/dashboard এ একটি project তৈরি করুন।
২. Project Settings > API থেকে Project URL এবং anon/public key নিন। এগুলো index.html ও admin.html-এর SUPABASE_URL এবং SUPABASE_ANON_KEY ঘরে বসান। Secret/service_role key কখনো ব্রাউজারের ফাইলে বসাবেন না।
৩. Supabase > SQL Editor-এ supabase-setup.sql-এর সম্পূর্ণ লেখা paste করে Run করুন।
৪. Authentication > Users থেকে নিজের ইমেইল দিয়ে user তৈরি করুন।
৫. SQL Editor-এ এই query চালান (ইমেইল নিজেরটি দিয়ে বদলাবেন):
   insert into public.admin_users (user_id) select id from auth.users where email = 'আপনার-ইমেইল';
৬. Storage > New bucket থেকে cnc-gallery নামে PUBLIC bucket তৈরি করুন।
৭. পুরো ফোল্ডার Netlify-তে deploy করুন।
৮. সাইট ও admin.html পরীক্ষা করুন। সব ঠিক হলে মূল URL দিয়ে QR কোড বানাবেন।

নিরাপত্তা নোট
- Supabase anon/publishable key ক্লায়েন্টে থাকা স্বাভাবিক; RLS নীতি ডেটা সুরক্ষা দেয়।
- service_role/secret key কখনো প্রকাশ করবেন না।
- অ্যাডমিন ইমেইল ও পাসওয়ার্ড আপনার নিজের হবে; কাউকে শেয়ার করবেন না।
- প্যাকেজের কোড তৈরি করা হয়েছে, কিন্তু আপনার Supabase/Netlify অ্যাকাউন্টে কোনো সেটআপ বা প্রকাশনা করা হয়নি।
