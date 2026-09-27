# KSAKit 🇸🇦

مكتبة TypeScript/JavaScript خفيفة للمشاريع السعودية. تتعامل مع الأرقام العربية والإنجليزية والمختلطة، أرقام الجوال السعودية، IBAN، الرقم الضريبي، الريال السعودي، وتنظيف النص العربي.

> Developer utilities built for Saudi applications.

## Install
```bash
npm install ksakit
```

## Quick start
```ts
import { ksa } from 'ksakit';

ksa.numbers.toEnglish('٠٥٥١٢٣٤٥٦٧'); // 0551234567
ksa.phone.isValid('٠٥٥ ١٢٣ ٤٥٦٧');   // true
ksa.phone.international('0551234567'); // +966551234567
ksa.iban.isValid('SA03 8000 0000 6080 1016 7519'); // true
ksa.vat.isValid('310123456700003'); // true
ksa.currency.parse('١٤٩٫٥٠ ريال'); // 149.5
ksa.currency.format(149); // SAR formatted using Intl
ksa.text.normalizeArabic('أَحْمَد  الـحربي'); // احمد الحربي
```

## Numbers
يدعم الأرقام العربية `٠١٢٣` والفارسية/الشرقية `۰۱۲۳` والإنجليزية، حتى لو كانت مختلطة في نفس النص.

```ts
ksa.numbers.toEnglish('٠۵٥١2٣٤56٧'); // 0551234567
ksa.numbers.toArabic('149'); // ١٤٩
ksa.numbers.normalize('السعر ١٤٩٫٥٠'); // السعر 149.50
```

## Saudi phone
يقبل الصيغ الشائعة مثل `05...`, `5...`, `966...`, `+966...`, `00966...` ثم يوحدها إلى الصيغة المحلية.

## Saudi IBAN
التطبيع + فحص بنية IBAN السعودية + checksum القياسي Mod-97.

## VAT
يتحقق حاليًا من البنية الأساسية للرقم الضريبي السعودي: 15 رقمًا يبدأ وينتهي بـ3. هذا **ليس** تحققًا من تسجيل المنشأة لدى ZATCA.

## Arabic text
`normalizeArabic()` يزيل التشكيل والتطويل ويوحد أشكال الألف و`ى` لتسهيل البحث والمقارنة. لا تستخدمه إذا كنت تحتاج الحفاظ على الإملاء الأصلي.

## API
- `ksa.numbers.toEnglish(value)`
- `ksa.numbers.toArabic(value)`
- `ksa.numbers.normalize(value)`
- `ksa.phone.normalize(value)`
- `ksa.phone.isValid(value)`
- `ksa.phone.international(value)`
- `ksa.iban.normalize(value)` / `isValid()` / `format()`
- `ksa.vat.normalize(value)` / `isValid()`
- `ksa.currency.parse(value)` / `format(value, locale?)`
- `ksa.text.normalizeArabic(value)` / `removeDiacritics(value)`

## Development
```bash
npm install
npm test
npm run typecheck
npm run build
```

## Roadmap
National/address helpers and additional Saudi-specific utilities can be added after their rules and official constraints are verified. Avoid treating local format checks as government verification.

## License
MIT
