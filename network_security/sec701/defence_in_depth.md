# Defense in Depth Network

<p align ="center">
    <img src= "/network_security/photo/defence_in_depth.svg" alt = "cloud deployment"
</p>


هي **استراتيجية أمنية** بتقول إننا ماينفعش نعتمد على طبقة واحدة من الحماية (مثلاً Firewall بس).

لازم نعمل **طبقات متتالية من الدفاع** بحيث لو هجوم اخترق طبقة يلاقي طبقة تانية توقفه.

زي فكرة **البصل** 🧅: كل طبقة حماية حوالين البيانات المهمة.


### Defense in Depth Levels
#### **Perimeter Security (الأطراف)**

دي أول طبقة، زي
**Firewall, IDS/IPS, VPN gateways**

هدفها تمنع الدخول غير المصرّح بيه من الإنترنت.



#### **Network Segmentation (التقسيم الداخلي)**

بدل ما تبقى كل الشبكة مع بعضها، نقسمها
VLANs / Subnets (IT, HR, DB, DMZ).

كده لو حد اخترق جزء، ما يقدرش يتحرك بسهولة لباقي الشبكة 


#### **DMZ (Demilitarized Zone)**

منطقة معزولة نحط فيها الخدمات اللي لازم تكون متاحة للعالم الخارجي زي
- Web
- Email

معزولة عن الشبكة الداخلية علشان حتى لو اتخترقت، داخل الشبكه يفضل آمن.


#### **Endpoint Security (الأجهزة)**

حماية على مستوى الأجهزة نفسها: Antivirus, EDR, Patching.

لأن الهجوم ممكن يحصل من جهاز مستخدم جوة الشبكة مش بس من برة.

الهدف مش بس المنع، لكن **الاكتشاف السريع** للهجمات.


#### **Policies & Awareness (العنصر البشري)**
تدريب الموظفين ضد Phishing و Social Engineering.

---


1- Inside can talk to Outside and outside can only reply to inside

**الداخل يقدر يبدأ اتصال مع الخارج** (مثلاً موظف يفتح موقع على الإنترنت).
**الخارج يرد فقط** (الردود مسموحة لأن الجدار الناري Stateful).

2- Outside Can not start conversation with inside

اي محاولة من الإنترنت عشان يبدأ اتصال مباشر مع الشبكة الداخلية **مرفوضة تمامًا**

3- Outside can talk to DMZ and DMZ can only reply to Outside

الإنترنت مسموح له يتكلم مع الـ DMZ **في بورتات محددة فقط** زي
- HTTP/HTTPS 
- Web 
- SMTP 
- Email

السيرفرات في الـDMZ **ترد بس، ما تبدأش اتصال**.

4- DMZ can not start conversation with Outside

السيرفرات في الـDMZ **ما تبادرش بإنشاء اتصال جديد** مع الإنترنت (علشان ما تستخدمش كنقطة انطلاق لهجوم).


5- There is no Policy between IN -> DMZ

بما إن مفيش سياسه بين Inside و DMZ، ده معناه إن **مفيش تواصل مباشر**.

أي اتصال لازم يتعمله Explicit Policy لو الشركة عايزة (مثلاً: Admins يدخلوا على الـWeb Server للإدارة).
