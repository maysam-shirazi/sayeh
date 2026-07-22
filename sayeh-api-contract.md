# Sayeh API Contract

Version: 0.3 (contract — every endpoint below is required to return the documented shape at 200; current backend gaps tracked separately in [§11](#sec-11), see [§10](#sec-10) changelog)
Base URL: `https://<host>/bapi`
Auth: Bearer token (`Authorization: Bearer <token>`)

> ⚠ **Base URL fix**: table paths below already start with `/sayeh/...` — do NOT
> put `/sayeh` in Base URL too (previous v0.2 had `.../bapi/sayeh/` + `/sayeh/...`
> paths = double prefix, every call would 404). Base URL is just the gateway
> root, paths carry the rest.

---

<a id="sec-1"></a>
## 1. Auth (`/sayeh/auth/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| [USER_PERMISSION](#sec-7-1) | GET | `/sayeh/auth/user_permission/` | دسترسی کاربر | DONE — [§7.1](#sec-7-1) |
| [AUTH_SESSIONS](#sec-7-2) | GET | `/sayeh/auth/sessions/` | نشست های فعال من | DONE — [§7.2](#sec-7-2) |
| [AUTH_SESSION_CLOSE](#sec-7-3) | DELETE | `/sayeh/auth/sessions/close/` | خاتمه نشست من | DONE — [§7.3](#sec-7-3) |
| [LOGIN_LOGOUT_REPORT](#sec-7-4) | GET | `/sayeh/auth/login_logout_report/` | گزارش ورود و خروج من | DONE — [§7.4](#sec-7-4) |
| [CHANGE_PASSWORD](#sec-7-5) | POST | `/sayeh/auth/change_password/` | تغییر گذرواژه | DONE — [§7.5](#sec-7-5) |
| [PROFILE](#sec-7-6) | GET | `/sayeh/auth/profile/` | پروفایل | DONE — [§7.6](#sec-7-6) |
| [REGISTRATION_ACCESS](#sec-7-7) | POST | `/sayeh/auth/registration_access/` | (no name) | DONE — [§7.7](#sec-7-7) |
| [REGISTER_USER](#sec-7-8) | POST | `/sayeh/auth/register_user/` | ثبت نام کاربر | PARTIAL — [§7.8](#sec-7-8), body TBD (depends on OTP flow [§7.13](#sec-7-13)/[§7.14](#sec-7-14)) |

---

<a id="sec-2"></a>
## 2. Manage (`/sayeh/manage/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| [GROUP_MGMT](#sec-7-9) | GET/POST/PUT/DELETE/PATCH | `/sayeh/manage/group_mgmt/` | گروه های کاربری | DONE — [§7.9](#sec-7-9), PATCH payload change required ([§9.4](#sec-9-4)#13) |
| [PERMISSION_MGMT](#sec-7-10) | GET | `/sayeh/manage/permission_mgmt/` | لیست دسترسی سطوح دسترسی | DONE — [§7.10](#sec-7-10) |
| [ROLE_MGMT](#sec-7-11) | GET/POST/PUT/DELETE | `/sayeh/manage/role_mgmt/` | سطح دسترسی | DONE — [§7.11](#sec-7-11) |
| [ACCOUNT_MGMT](#account_mgmt-get) | GET/POST | `/sayeh/manage/account_mgmt/` | لیست/ایجاد کاربر | DONE — [§6.1](#account_mgmt-get)/[§6.1b](#account_mgmt-post) |
| [ACCOUNT_MGMT](#account_mgmt-put) | PATCH | `/sayeh/manage/account_mgmt/{id}/` | ویرایش کاربر | DONE — [§6.1c](#account_mgmt-put), was PUT ([§9.4](#sec-9-4)) |
| [ACCOUNT_MGMT_PROFILES](#account_mgmt-profiles-get) | GET/POST/PATCH | `/sayeh/manage/account_mgmt/{id}/profiles/` | پروفایل کاربر | DONE — [§6.2](#account_mgmt-profiles-get)/[§6.2b](#account_mgmt-profiles-post)/[§6.2c](#account_mgmt-profiles-put), was PUT ([§9.4](#sec-9-4)) |
| [PROFILE_GROUPS](#profile-groups-post) | POST/DELETE | `/sayeh/manage/profile/{profile_id}/groups/` | تخصیص/حذف گروه | DONE — [§6.3](#profile-groups-post) (confirmed model, see [§9.1](#sec-9-1)) |
| [PROFILE_ROLES](#profile-roles-post) | POST/DELETE | `/sayeh/manage/profile/{profile_id}/roles/` | تخصیص/حذف نقش | DONE — [§6.4](#profile-roles-post) |
| [ACCOUNT_MGMT_CONTACT](#account_mgmt-contact-put) | PATCH | `/sayeh/manage/account_mgmt/{id}/contact/` | ویرایش اطلاعات تماس | DONE — [§6.5](#account_mgmt-contact-put), was PUT ([§9.4](#sec-9-4)) |
| [PROTECTED_RESOURCE_MGMT](#sec-7-12) | GET | `/sayeh/manage/protected_resource_mgmt/` | سامانه‌های حفاظت شده | DONE — [§7.12](#sec-7-12) |
| [SUBCATALOGFIELD_MGMT](#sec-7-13) | GET | `/sayeh/manage/subcatalogfield_mgmt/` | فیلد های زیرمجموعه کاتالوگ | DONE — [§7.13](#sec-7-13) |
| [ACCESS_POLICY_MGMT](#sec-7-14) | GET/POST/PUT/DELETE | `/sayeh/manage/access_policy_mgmt/` | سیاست های دسترسی | DONE — [§7.14](#sec-7-14), architecture question re role-model overlap ([§9.2](#sec-9-2)) |
| [CONDITION_MGMT](#sec-7-15) | GET/POST/PUT/DELETE | `/sayeh/manage/condition_mgmt/` | شرایط سیاست دسترسی | DONE — [§7.15](#sec-7-15) |
| [ACCOUNT_ACTION_MGMT](#sec-7-16) | GET | `/sayeh/manage/account_action_mgmt/` | لاگ های فراخوانی وب سرویس | DONE — [§7.16](#sec-7-16), ⚠ `data` field non-JSON, see [§9](#sec-9) |

---

<a id="sec-3"></a>
## 3. Base (`/sayeh/base/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| [SYSTEM_SUBCATALOG](#sec-7-17) | GET | `/sayeh/base/get_system_subcatalog/` | زیرمجموعه کاتالوگ سیستمی | DONE — [§7.17](#sec-7-17) |
| [CAS_AUDIT_LOG](#sec-7-18) | GET | `/sayeh/base/cas_audit_log/` | لاگ های ورود و خروج سیستم | DONE — [§7.18](#sec-7-18) |
| [CAS_AUDIT_LOG_AGGRS](#sec-7-19) | GET | `/sayeh/base/cas_audit_log_aggrs/` | تجمیع لاگ های احراز هویت | DONE — [§7.19](#sec-7-19) |
| [SEND_OTP](#sec-7-20) | POST | `/sayeh/base/send_otp/` | ارسال کد تایید | DONE — [§7.20](#sec-7-20), public endpoint (no auth) |
| [VALIDATE_OTP](#sec-7-21) | POST | `/sayeh/base/validate_otp/` | اعتبارسنجی کد تایید | DONE — [§7.21](#sec-7-21), changed GET→POST |
| [INITIAL_CONFIGS](#sec-7-22) | GET | `/sayeh/base/initial_configs/` | اطلاعات اولیه ثبت نام | DONE — [§7.22](#sec-7-22), ⚠ typo in response, see [§9](#sec-9) |

---

<a id="sec-4"></a>
## 4. Admin (`/sayeh/admin/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| [SAYEH_DASHBOARD_OVERVIEW](#sec-7-23) | GET | `/sayeh/admin/sayeh_dashboard_overview/` | آمار کلی داشبورد تنظیمات | DONE — [§7.23](#sec-7-23) |

---

<a id="sec-5"></a>
## 5. SSO (`/sayeh/sso/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| [OIDC_CREDENTIAL](#sec-7-24) | GET | `/sayeh/sso/oidc_credential/` | تنظیمات OIDC (نام قبلی: LOGOUT — نادرست، [§9](#sec-9)) | DONE — [§7.24](#sec-7-24) |
| [USER_CREDENTIAL_MANAGEMENT](#sec-7-25) | POST | `/sayeh/sso/user_credential_management/` | احراز هویت توکن لاگین متمرکز | PARTIAL — [§7.25](#sec-7-25), body TBD |

---

<a id="sec-6"></a>
## 6. Account / Profile Endpoint Details

<a id="account_mgmt-get"></a>
### 6.1 ACCOUNT_MGMT

`GET /sayeh/manage/account_mgmt/?id={id}`

**Headers:** `Authorization: Bearer <token>`

**Query params**
- `id` (int, required) — account id

**Success 200 — simplified for UI**
```json
{
  "id": 12,
  "uid": "0012345678",
  "domain": "DIRECTORY_SERVICE_ENVIRONMENT",
  "is_active": true,
  "is_mfa": false,
  "is_registered": true,
  "identification_code": "117",
  "contact": {
    "mobile": "09914563211",
    "mobile_verified": true,
    "email": "ali@gmail.com",
    "email_verified": false,
    "country": null,
    "city": null,
    "postal_code": null,
    "address": null,
    "org_mobile": null,
    "org_email": null
  },
  "identity": {
    "name": "علی",
    "surname": "موسوی",
    "en_name": "mamahd",
    "en_surname": "ahmadi",
    "gender": "male",
    "father_name": "ali",
    "birth_date": "2026-07-06",
    "national_code": "0012345678"
  },
  "profile": {
    "id": 13,
    "title": "علی موسوی",
    "is_active": true,
    "type": "پرسنل",
    "roles": []
  }
}
```

**Errors**
- `404 ACCOUNT_NOT_FOUND` — bad id
- `401 UNAUTHORIZED`

**Changes from raw backend response — why**
- Dropped `__` prefix flatten (`contact_info__mobile` → `contact.mobile`) — nest instead, easier for front to consume
- Top-level `identity` object built from `profiles__identity__*` fields
- Removed account-level `roles`/`role_objects` — per [§12](#sec-12) model, roles belong to profile not account, backend leak
- **Removed account-level `groups`** (was `user_groups_data` in raw response) — per [§9.1](#sec-9-1), group membership confirmed profile-only, this field was a backend leak same category as `roles`. Group info now lives solely under `profile.groups` ([§6.2](#account_mgmt-profiles-get)/[§6.3](#profile-groups-post))
- Dropped `over_view` block — account-list-level stats, not single-account data
- Dropped `profile_data` array, `total_count`, dup id refs — full profile list moved to [§6.2](#account_mgmt-profiles-get)
- Added `profile` — the `is_default: true` profile embedded inline, front needs active-profile context on load
- `profiles__identification_code` duplicate of top-level, kept once

**Edge case:** account with zero profiles — `profile` should be `null`, front must handle "no active profile" state.

---

<a id="account_mgmt-post"></a>
### 6.1b ACCOUNT_MGMT — create

`POST /sayeh/manage/account_mgmt/`

**Headers:** `Authorization: Bearer <token>`

**Request body**
```json
{
  "uid": "0012345678",
  "domain": "DIRECTORY_SERVICE_ENVIRONMENT",
  "is_active": true,
  "is_mfa": false,
  "contact": {
    "mobile": "09914563211",
    "email": "ali@gmail.com",
    "country": null,
    "city": null,
    "postal_code": null,
    "address": null,
    "org_mobile": null,
    "org_email": null
  },
  "identity": {
    "name": "علی",
    "surname": "موسوی",
    "en_name": "mamahd",
    "en_surname": "ahmadi",
    "gender": "male",
    "father_name": "ali",
    "birth_date": "2026-07-06",
    "national_code": "0012345678"
  }
}
```

**Success 201** — same shape as [§6.1](#account_mgmt-get) GET response

**Errors**
- `422 VALIDATION_ERROR`
- `409 UID_TAKEN`
- `409 NATIONAL_CODE_TAKEN`
- `401 UNAUTHORIZED`

**Notes**
- No `profile` in request — created without profile, `profile: null` until profile-create called
- `is_active`/`is_mfa` optional — defaults resolved: `is_active: true`, `is_mfa: false` if omitted, see [§9.4](#sec-9-4) item 4
- `mobile_verified`/`email_verified` set `false` server-side, confirmed via OTP flow separately

---

<a id="account_mgmt-put"></a>
### 6.1c ACCOUNT_MGMT — update

`PATCH /sayeh/manage/account_mgmt/{id}/` — changed from PUT, see [§9.4](#sec-9-4) item 1

**Headers:** `Authorization: Bearer <token>`

**Request body** — partial, send only fields being changed
```json
{
  "contact": { "mobile": "09914563211" }
}
```
Any top-level or nested field may be included; omitted fields stay unchanged server-side.

**Success 200** — updated resource, same shape as [§6.1](#account_mgmt-get) GET response

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `409 NATIONAL_CODE_TAKEN`
- `401 UNAUTHORIZED`

---

<a id="account_mgmt-profiles-get"></a>
### 6.2 ACCOUNT_MGMT — profiles

`GET /sayeh/manage/account_mgmt/{id}/profiles/`

**Headers:** `Authorization: Bearer <token>`

**Success 200 — simplified for UI**
```json
{
  "profiles": [
    {
      "id": 13,
      "title": "علی موسوی",
      "is_active": true,
      "is_default": true,
      "type": "پرسنل",
      "type_id": 79,
      "identification_code": "117",
      "groups": [
        { "id": 1, "title": "کارکنان" }
      ],
      "units": []
    }
  ]
}
```

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `401 UNAUTHORIZED`

**Notes:** Dropped `sayeh_account` (redundant), merged split id/title arrays into objects. Added `type_id` alongside `type` text, see [§9.4](#sec-9-4) item 3.

**Resolved:** array wrapper `{profiles:[...]}` kept permanently, even for single-profile accounts — see [§9.4](#sec-9-4) item 2.

---

<a id="account_mgmt-profiles-post"></a>
### 6.2b ACCOUNT_MGMT — profile create

`POST /sayeh/manage/account_mgmt/{account_id}/profiles/`

**Request body**
```json
{
  "title": "علی موسوی",
  "type_id": 79,
  "identification_code": "117",
  "is_active": true,
  "is_default": false
}
```

**Success 201** — profile object, same shape as [§6.2](#account_mgmt-profiles-get) list entry plus `roles: []` (includes both `type` text and `type_id`)

**Errors**
- `422 VALIDATION_ERROR`
- `404 ACCOUNT_NOT_FOUND`
- `401 UNAUTHORIZED`

**Notes:** `type_id` sent as numeric id (matches [§7.13](#sec-7-13) SUBCATALOGFIELD_MGMT catalog `ORG_IDENTITY_TYPE`/similar), response returns text `type` too, see [§9.4](#sec-9-4) item 3. No `groups`/`roles` in create body, assign after via [§6.3](#profile-groups-post)/[§6.4](#profile-roles-post) (confirmed model, [§9.1](#sec-9-1)). `is_default: true` auto-unsets previous default server-side — required behavior, see [§9.4](#sec-9-4) item 5.

---

<a id="account_mgmt-profiles-put"></a>
### 6.2c ACCOUNT_MGMT — profile update

`PATCH /sayeh/manage/account_mgmt/{account_id}/profiles/{profile_id}/` — changed from PUT, see [§9.4](#sec-9-4) item 1

**Request body** — partial, send only changed fields
```json
{
  "title": "علی موسوی",
  "type_id": 79,
  "is_active": true,
  "is_default": false
}
```

**Success 200** — same shape as [§6.2b](#account_mgmt-profiles-post) response

**Errors**
- `404 PROFILE_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes:** `identification_code` excluded, assume immutable. `type_id` used here (not `type`) since request needs the numeric id — response still returns both `type` (text) and `type_id`, see [§9.4](#sec-9-4) item 3.

---

<a id="profile-groups-post"></a>
### 6.3 Profile — group assign / unassign — **CONFIRMED per [§9.1](#sec-9-1)**

Group membership confirmed profile-only ([§9.1](#sec-9-1)). Real `GROUP_MGMT` PATCH ([§7.9](#sec-7-9)) using `sayeh_accounts` is a backend mismatch, flagged to fix — front should NOT call it as-is; use endpoints below.

`POST /sayeh/manage/profile/{profile_id}/groups/`
```json
{ "group_id": 1 }
```
**Success 201**
```json
{ "id": 1, "title": "کارکنان" }
```

`DELETE /sayeh/manage/profile/{profile_id}/groups/{group_id}/`
**Success 204** — no body

**Errors (both)**
- `404 PROFILE_NOT_FOUND` / `404 GROUP_NOT_FOUND`
- `409 ALREADY_ASSIGNED` — POST only
- `401 UNAUTHORIZED`

**Notes:** Assigning group affects aggregated `roles` on profile ([§9](#sec-9), group→role inheritance) — refetch profile detail ([§6.2](#account_mgmt-profiles-get)) after write, don't compute client-side. Exact route still needs backend confirm/build (not in original URL list) — but semantics (profile joins group) now locked in.

---

<a id="profile-roles-post"></a>
### 6.4 Profile — direct role assign / unassign

`POST /sayeh/manage/profile/{profile_id}/roles/`
```json
{ "role_id": 5 }
```
**Success 201**
```json
{ "id": 5, "title": "مدیر گروه" }
```

`DELETE /sayeh/manage/profile/{profile_id}/roles/{role_id}/`
**Success 204** — no body

**Errors (both)**
- `404 PROFILE_NOT_FOUND` / `404 ROLE_NOT_FOUND`
- `409 ALREADY_ASSIGNED` — POST only
- `401 UNAUTHORIZED`

**Notes:** Direct role assign only, distinct from group-inherited roles ([§6.3](#profile-groups-post)/[§9](#sec-9)). This one not contradicted by real data — roles do live separate from groups per [§7.11](#sec-7-11) ROLE_MGMT shape (`permissions` array on role, no account/profile ref) — assignment endpoint itself still needs real confirm, shape of relationship looks right though.

---

<a id="account_mgmt-contact-put"></a>
### 6.5 ACCOUNT_MGMT — contact info update

`PATCH /sayeh/manage/account_mgmt/{id}/contact/` — changed from PUT, see [§9.4](#sec-9-4) item 1 (anchor id kept as `-put` for link stability)

**Request body — non-verified fields only, partial**
```json
{
  "city": "تهران"
}
```
Any subset of the non-verified fields may be sent; omitted fields stay unchanged.

**Success 200** — updated contact object

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes:** `mobile`/`email` excluded on purpose, go through OTP flow ([§7.20](#sec-7-20)/[§7.21](#sec-7-21)) so `mobile_verified`/`email_verified` stay trustworthy.

---

<a id="sec-7"></a>
## 7. Endpoint Details — Auth / Manage / Base / Admin / SSO

<a id="sec-7-1"></a>
### 7.1 USER_PERMISSION

`GET /sayeh/auth/user_permission/`

**Success 200**
```json
{
  "status": "SUCCESS",
  "user_permissions": ["SUPER_USER_PERMISSION"]
}
```
**Notes:** Flat array of permission code strings. `SUPER_USER_PERMISSION` = all-access bypass.

---

<a id="sec-7-2"></a>
### 7.2 AUTH_SESSIONS

`GET /sayeh/auth/sessions/`

**Success 200**
```json
{
  "count": 5,
  "result": [
    {
      "id": "ac9f2947-bcd5-4559-9b80-be69cc9e6710",
      "date_created": "2026-07-22T06:59:08.693795+00:00",
      "last_activity": "2026-07-22T08:05:15.022496+00:00",
      "is_current": true,
      "is_active": true
    }
  ]
}
```
**Notes:** `id` is session UUID. `is_current` true for token used in this request.

---

<a id="sec-7-3"></a>
### 7.3 AUTH_SESSION_CLOSE

`DELETE /sayeh/auth/sessions/close/?id={session_id}`

**Success 200**
```json
{ "detail": "نشست بسته شد." }
```
**Errors:** `401` — token invalid (e.g. already closed)

**Notes:** Revokes SSO token server-side, deletes session. Cannot close current request's own session (token invalidates after).

---

<a id="sec-7-4"></a>
### 7.4 LOGIN_LOGOUT_REPORT

`GET /sayeh/auth/login_logout_report/`

**Success 200**
```json
{
  "count": 83,
  "result": [
    {
      "@timestamp": "2026-07-21T13:53:06.312+03:30",
      "serviceId": null,
      "reason": "SINGLE_LOGOUT_SERVICES",
      "clientIp": "192.168.241.189",
      "userAgent": "Mozilla/5.0 ...",
      "authorized": true
    }
  ]
}
```
**Notes:** Elasticsearch audit entries. `serviceId` = protected resource id (null for logout events).

---

<a id="sec-7-5"></a>
### 7.5 CHANGE_PASSWORD

`POST /sayeh/auth/change_password/`

**Request body**
```json
{
  "old_password": "current_pass",
  "new_password": "new_pass",
  "new_password_confirmation": "new_pass"
}
```
**Success 200**
```json
{ "detail": "گذرواژه با موفقیت تغییر کرد." }
```
**Errors:** `400` — field-level validation errors object

---

<a id="sec-7-6"></a>
### 7.6 PROFILE

`GET /sayeh/auth/profile/`

Same shape as [§6.1](#account_mgmt-get) GET response — full account+profile+groups+roles for currently authenticated user.

---

<a id="sec-7-7"></a>
### 7.7 REGISTRATION_ACCESS

`POST /sayeh/auth/registration_access/`

**Request body**
```json
{ "national_code": "0012345678" }
```
**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Errors:** `400` — bad params

**Notes:** Checks national-code eligibility before registration.

---

<a id="sec-7-8"></a>
### 7.8 REGISTER_USER — PARTIAL, body TBD

`POST /sayeh/auth/register_user/`

**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Errors:** `400` — bad params

**Notes:** Requires OTP flow first ([§7.20](#sec-7-20)/[§7.21](#sec-7-21)). Exact request body depends on registration type (self vs gov) — not yet nailed down, don't build against this until confirmed.

---

<a id="sec-7-9"></a>
### 7.9 GROUP_MGMT

`GET /sayeh/manage/group_mgmt/?page_size={n}&page={n}`

**Success 200 — list**
```json
{
  "status": "PASS",
  "data": [
    { "id": 1, "groups": [1], "code": "PERSONEL", "title": "کارکنان", "is_active": true, "description": "گروه کارکنان" }
  ],
  "total_count": 1
}
```

**POST** — create: `{ "code": "NEW_GROUP", "title": "New Group", "description": "test" }`
**PUT** (`?id={id}`) — update: `{ "code": "GROUP_CODE", "title": "Updated Title", "description": "Updated desc" }`
**DELETE** (`?id={id}`)
**PATCH** — membership (target shape, backend fix pending): `{ "sayeh_profiles": [profile_id], "action": "ADD_PROFILE" | "REMOVE_PROFILE" }` — live endpoint currently takes `sayeh_accounts`/`ADD_ACCOUNT`/`REMOVE_ACCOUNT`, see resolution below

**Resolved:** PATCH must take profile ids, not account ids — matches confirmed [§9.1](#sec-9-1) profile-only group membership. Live behavior (`sayeh_accounts`) contradicts this, backend needs to rewire, see [§9.4](#sec-9-4) item 13. Front should not build against the account-based version.

**Contract requirement:** must return `200` with the shape above — current deployment returns `500` (`{"detail": "خطای داخلی سرور رخ داده است."}`), tracked as an open backend task in [§11](#sec-11), not a spec ambiguity. Shape confirmed from other test env.

---

<a id="sec-7-10"></a>
### 7.10 PERMISSION_MGMT

`GET /sayeh/manage/permission_mgmt/?page={n}&page_size={n}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    { "id": 1, "code": "PERM_1", "title": "Permission 1", "description": "...", "parent": null }
  ],
  "total_count": 1
}
```
**Notes:** Hierarchical parent-child. `description` encodes `"{path}-{method}"` for API-level perms.

---

<a id="sec-7-11"></a>
### 7.11 ROLE_MGMT

`GET /sayeh/manage/role_mgmt/?page={n}&page_size={n}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    { "id": 1, "code": "SUPER_ADMIN", "title": "SUPER_ADMIN", "permissions": [1, 2, 3] }
  ],
  "total_count": 1
}
```

**POST** — `{ "code": "NEW_ROLE", "title": "New Role", "permissions": [1, 2] }`
**PUT** (`?id={id}`) — `{ "title": "Updated Title", "permissions": [1], "code": "ROLE_CODE" }`
**DELETE** (`?id={id}`)

**Resolved:** use `permissions` (plural) consistently — GET response and POST/PUT body both, was `permission` singular on write before, see [§9.4](#sec-9-4) item 8.

---

<a id="sec-7-12"></a>
### 7.12 PROTECTED_RESOURCE_MGMT

`GET /sayeh/manage/protected_resource_mgmt/?page_size={n}&page={n}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    {
      "id": 21, "groups": [], "code": "MY_REFAH", "title": "MY_REFAH",
      "description": "درگاه خدمات سازمانی", "is_active": true, "is_mfa": false,
      "order": 1, "gov_exclusive": false, "sso_protocol": 1, "oauth_client_id": null,
      "resource_uri": "https://my.refahbank.net/user/oauth", "logout_url": null,
      "redirect_link": null, "scope": null, "type": null, "visible": true,
      "has_subpath": false, "resource_logo": "resource_logos/...",
      "access_policy": [1, 2], "protected_resource_type": [47]
    }
  ],
  "total_count": 1
}
```

---

<a id="sec-7-13"></a>
### 7.13 SUBCATALOGFIELD_MGMT

`GET /sayeh/manage/subcatalogfield_mgmt/?catalog__code={code}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    { "id": 79, "code": "STAFF", "title": "پرسنل", "description": null, "catalog": 5 }
  ],
  "total_count": 1
}
```
**Errors:** `400` — `{"status": "FAIL", "message": "catalog_code is required"}`

**Notes:** Backs profile `type` picker ([§6.2b](#account_mgmt-profiles-post)) — `catalog__code` values seen: `ORG_IDENTITY_TYPE`, `PROTECTED_RESOURCE_TYPE`.

---

<a id="sec-7-14"></a>
### 7.14 ACCESS_POLICY_MGMT

`GET /sayeh/manage/access_policy_mgmt/?page_size={n}&page={n}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    { "id": 1, "groups": [1], "code": "AP_1", "title": "Default Allow", "is_active": true, "effect": "allow", "priority": 100, "description": null }
  ],
  "total_count": 2
}
```
**POST/PUT/DELETE** — standard CRUD, see raw fields above.

**⚠ Architecture question:** this is effect+priority+condition based access control (ABAC-ish), separate from role→permission model ([§12](#sec-12)). Both systems exist simultaneously — unclear if access-policy can override a role grant, is evaluated first/last, or is fully independent layer for a different resource type (protected_resource, not app permission). Needs an architecture decision doc, not just endpoint spec — flag for backend/architect discussion before front builds any policy-editing UI.

---

<a id="sec-7-15"></a>
### 7.15 CONDITION_MGMT

`GET /sayeh/manage/condition_mgmt/?page_size={n}&page={n}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    {
      "id": 1, "access_policy": 1, "title": "Business Hours", "type": "timerange_condition",
      "operand": "range", "is_active": true, "ip_condition_value": null,
      "date_condition_value": null, "weekday_condition_value": null,
      "timerange_condition_value": "08:00:00,17:00:00", "username_condition_value": null
    }
  ],
  "total_count": 1
}
```
**POST/PUT/DELETE** — standard CRUD.

**Notes:** Condition types: `timerange_condition`, `date_condition`, others likely exist (`ip_condition`, `weekday_condition`, `username_condition` implied by null fields) — confirm full enum.

---

<a id="sec-7-16"></a>
### 7.16 ACCOUNT_ACTION_MGMT

`GET /sayeh/manage/account_action_mgmt/?scope={scope}`

**Query params:** `scope` (required) — `ALL` or `USER`

**Success 200 — target shape (backend fix pending, see below)**
```json
{
  "data": [
    {
      "id": 569, "sayeh_account_uid": "my_admin", "status": true,
      "data": { "page_size": ["500"] }, "message": "دریافت گروه",
      "action_type": "مدیریت گروه ها", "ip": "192.168.240.16",
      "user_agent": "Mozilla/5.0 ...", "object_id": null,
      "date_created": "2026-07-22T08:04:44.936113Z", "admin": null
    }
  ],
  "total_count": 569
}
```
**Errors:** `400` — `{"status": "FAIL", "message": "invalid scope"}`

**Resolved:** `data` must be a real JSON object, not a Python `repr()` string — live response currently returns `"data": "{'page_size': ['500']}"` (single-quoted, invalid JSON syntax embedded in a JSON string). Backend needs to serialize with `json.dumps()`/native object instead of `str(dict)`. Front will treat `data` as an object per this target shape, see [§9.4](#sec-9-4) item 10.

---

<a id="sec-7-17"></a>
### 7.17 SYSTEM_SUBCATALOG

`GET /sayeh/base/get_system_subcatalog/?catalog_code={code}`

**Success 200**
```json
{
  "status": "PASS",
  "data": [
    { "id": 1, "code": "CAS", "title": "CAS", "description": null, "catalog_id": 1, "is_active": true },
    { "id": 2, "code": "OAUTH2", "title": "OAUTH2", "description": null, "catalog_id": 1, "is_active": true }
  ]
}
```
**Errors:** `400` — `{"status": "FAIL", "message": "Bad parameter"}`

---

<a id="sec-7-18"></a>
### 7.18 CAS_AUDIT_LOG

`GET /sayeh/base/cas_audit_log/?page={n}&page_size={n}`

**Success 200**
```json
{ "result": [], "count": 0 }
```
**Notes:** May be empty if no CAS auth events in configured window.

---

<a id="sec-7-19"></a>
### 7.19 CAS_AUDIT_LOG_AGGRS

`GET /sayeh/base/cas_audit_log_aggrs/?field={field_name}`

**Success 200 — target shape (backend fix pending)**
```json
{ "status": "SUCCESS", "data": [] }
```
**Errors:** `400` — `{"status": "FAIL", "message": "field must send"}`

**Resolved:** use lowercase `status` — live response currently returns uppercase `STATUS`, inconsistent with nearly every other endpoint. Backend to fix casing, see [§9.4](#sec-9-4) item 9.

---

<a id="sec-7-20"></a>
### 7.20 SEND_OTP — decided, see [§9.4](#sec-9-4) item 6

`POST /sayeh/base/send_otp/` — **must be public, no `Authorization` header required**

**Request body**
```json
{ "target": "mobile", "value": "09912345678" }
```
**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Resolved:** the `401` seen during earlier testing was a bug, not intended behavior — this endpoint is called before registration/login exists (no token available yet), so requiring a bearer token is a contradiction, not a design choice. Backend should remove any auth requirement here.

---

<a id="sec-7-21"></a>
### 7.21 VALIDATE_OTP — decided, see [§9.4](#sec-9-4) item 7

`POST /sayeh/base/validate_otp/` — **changed from GET to POST**, params move to request body

**Request body**
```json
{ "target": "mobile", "value": "09912345678", "code": "123456" }
```
**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Resolved:** GET-with-code-in-query was flagged risky (sensitive code ends up in access logs / browser history) — switched to POST with code in body. Same public-endpoint reasoning as [§7.20](#sec-7-20) likely applies here too (called pre-auth in registration flow), confirm with backend.

---

<a id="sec-7-22"></a>
### 7.22 INITIAL_CONFIGS

`GET /sayeh/base/initial_configs/` — no auth required (public)

**Success 200 — target shape (backend fix pending)**
```json
{
  "status": "success",
  "id_type": [
    { "id": 2, "code": "PERSONNEL_NO", "title": "کد پرسنلی", "description": "nationalCode" }
  ],
  "directory_services": [
    { "title": "مشخصات دایرکتوری شرکت", "code": "DIRECTORY_SERVICE_ENVIRONMENT" }
  ],
  "password_validation": [],
  "resource_category": [
    {
      "id": 47, "title": "سامانه ها", "code": "MDM", "description": "...",
      "is_active": true, "catalog": 1, "parent__id": null, "parent__title": null,
      "tag": "1", "comment": "media/resource_category_images/..."
    }
  ],
  "user_resources_data": [],
  "user_resources_count": 0
}
```

**Resolved:** fix `"susccess"` typo → `"success"`. Live response still has the typo — front should not string-match on it either way (check absence of `"FAIL"`/error instead), but backend should fix the source typo too, see [§9.4](#sec-9-4) item 11.

---

<a id="sec-7-23"></a>
### 7.23 SAYEH_DASHBOARD_OVERVIEW

`GET /sayeh/admin/sayeh_dashboard_overview/`

**Success 200 — target shape (backend fix pending)**
```json
{
  "data": {
    "total_users": 13, "active_users": 13, "total_roles": 1, "total_groups": 1,
    "protected_systems": 1, "access_policies": 2, "webservice_calls_today": 125,
    "units": 5, "announcements": 2, "failed_webservice_calls_today": 0, "failed_logins_today": 0
  }
}
```

**Resolved:** fix `annoncements` → `announcements`. Live field name currently has the typo, see [§9.4](#sec-9-4) item 12.

---

<a id="sec-7-24"></a>
### 7.24 OIDC_CREDENTIAL (renamed from LOGOUT — see [§9](#sec-9))

`GET /sayeh/sso/oidc_credential/`

**Success 200**
```json
{
  "oidc_credential": {
    "authority_base_url": "https://auth.refahbank.net",
    "authority": "https://auth.refahbank.net/oidc/authorize",
    "response_type": "code",
    "gov_client_id": "MY_REFAH",
    "redirect_uri": "https://my.refahbank.net/user/oauth",
    "scope": "tums",
    "org_client_id": "clientsecret-org"
  }
}
```
**Notes:** Returns OIDC config for SSO integration, used to build OAuth2 authorize URL. This is NOT a logout action despite old code name `LOGOUT` — renamed in table [§5](#sec-5), confirmed by response shape.

---

<a id="sec-7-25"></a>
### 7.25 USER_CREDENTIAL_MANAGEMENT — body TBD

`POST /sayeh/sso/user_credential_management/`

**Success 200**
```json
{ "detail": "..." }
```
**Errors:** `400` — JSON parse error if malformed

**Notes:** Token exchange for portal SSO. Request/response shape pending real integration test, don't build against this yet.

---

<a id="sec-8"></a>
## 8. Groups vs Profiles — architecture question (blocking, see [§9](#sec-9) for resolution needed)

(see [§9](#sec-9) below — kept as pointer since [§9](#sec-9) has full detail)

---

<a id="sec-9"></a>
## 9. Design Conflicts & Open Decisions — MUST RESOLVE BEFORE BUILD

<a id="sec-9-1"></a>
### 9.1 Who joins a group: Account or Profile? — **RESOLVED: Profile**

Confirmed: group membership belongs to **profile only**, not account. This means:

- [§6.3](#profile-groups-post) (`PROFILE_GROUPS`, profile joins group) is the **correct, authoritative** design — keep as-is, no longer tentative
- [§7.9](#sec-7-9) real `GROUP_MGMT` PATCH taking `sayeh_accounts` **contradicts confirmed model** — this is either:
  - a backend bug (endpoint should accept profile ids, not account ids — likely just named/wired wrong), or
  - a genuinely different feature (e.g. legacy bulk-assign, or an org-level grouping unrelated to permission-groups) that happens to share the `group_mgmt` path by accident
  - **Action:** flag to backend team as a bug/mismatch — `PATCH .../group_mgmt/` needs to take `sayeh_profiles` (or similar), not `sayeh_accounts`, to match confirmed design. Do not build front UI against the account-based PATCH as-is.
- [§6.1](#account_mgmt-get) account-level `groups` field (kept from raw response `user_groups_data`) is now **suspect** — if group membership is profile-only, this field is likely a backend leak/legacy join, same category as the `roles` field we already dropped from account. **Recommend dropping `groups` from account response too** ([§6.1](#account_mgmt-get)), rely on `profile.groups` (via [§6.2](#account_mgmt-profiles-get) profile detail) as sole source of truth. Flag to backend: is `user_groups_data` on the account serializer intentional or leftover?

Permission model ([§12](#sec-12)) confirmed as originally stated — no further changes needed there.

<a id="sec-9-2"></a>
### 9.2 Role/Permission model vs Access-Policy/Condition model — how do they interact?

[§7.11](#sec-7-11) ROLE_MGMT (role → list of permission ids) and [§7.14](#sec-7-14) ACCESS_POLICY_MGMT (effect/priority/condition rules) both look like authorization mechanisms but nothing in the raw data shows them referencing each other. Possibilities:
- Access-policy is scoped to `protected_resource` only (SSO gateway rules — "can this account reach this external system, and when") while role/permission is for in-app feature permissions — two separate concerns, not overlapping. Field `protected_resource_type: [access_policy: [1,2]]` in [§7.12](#sec-7-12) supports this reading.
- Or they're meant to merge into one evaluation eventually and aren't yet wired together

**Decision needed:** if reading 1 is correct (separate concerns), no conflict, just document clearly and move on. Confirm with backend before assuming.

<a id="sec-9-3"></a>
### 9.3 Naming/typo cleanup list (low priority, batch with backend later)
- `permissions` (GET) vs `permission` (POST/PUT) on ROLE_MGMT — [§7.11](#sec-7-11) — **RESOLVED, see §9.4**
- `STATUS` vs `status` casing — [§7.19](#sec-7-19) vs everywhere else — **RESOLVED, see §9.4**
- `"susccess"` typo — [§7.22](#sec-7-22) — **RESOLVED, see §9.4**
- `annoncements` typo — [§7.23](#sec-7-23) — **RESOLVED, see §9.4**
- `account_action_mgmt.data` field serialized as Python repr, not JSON — [§7.16](#sec-7-16) — **RESOLVED, see §9.4**

<a id="sec-9-4"></a>
### 9.4 Frontend-decided resolutions — ready for backend implementation

Everything below was an open question the frontend had discretion to call. Decided now so backend has one target to build, not a range of options. Items still needing backend/architect input (not frontend's call) are excluded — see [§9.2](#sec-9-2), still open.

| # | Item | Decision | Affects |
|---|---|---|---|
| 1 | PUT vs PATCH on account/profile/contact update | **PATCH**, partial-update semantics — only send changed fields, avoid full-object resend and stale-overwrite risk on concurrent edits | [§6.1c](#account_mgmt-put), [§6.2c](#account_mgmt-profiles-put), [§6.5](#account_mgmt-contact-put) |
| 2 | Profile list wrapper `{profiles:[...]}` vs bare object | **Keep array wrapper**, always — even if today every account has exactly one profile, don't special-case the shape; front parsing logic stays uniform, and multi-profile-per-account is explicitly part of the confirmed design ([§12](#sec-12)) so it will happen | [§6.2](#account_mgmt-profiles-get) |
| 3 | Profile `type` — text-only or text+id | **Both** — return `type` (display text) AND `type_id` (numeric) on every profile response (GET, create response, update response). Front edit-forms need the id to pre-select a dropdown without a second lookup call | [§6.2](#account_mgmt-profiles-get), [§6.2b](#account_mgmt-profiles-post), [§6.2c](#account_mgmt-profiles-put) |
| 4 | `is_active`/`is_mfa` defaults on account create | **`is_active: true`, `is_mfa: false`** if omitted from request body — document as explicit contract default, not implementation-defined | [§6.1b](#account_mgmt-post) |
| 5 | `is_default: true` on profile create/update | **Server auto-unsets previous default profile** in same transaction — front never has to make two calls to swap active profile | [§6.2b](#account_mgmt-profiles-post), [§6.2c](#account_mgmt-profiles-put) |
| 6 | SEND_OTP auth requirement | **Must be public, no bearer token required** — this is called before registration/login exists, a token requirement is a chicken-egg bug, not a design choice | [§7.20](#sec-7-20) |
| 7 | VALIDATE_OTP method | **Change GET → POST**, code + target go in request body not query string — avoids sensitive code landing in server access logs / browser history | [§7.21](#sec-7-21) |
| 8 | `permissions` vs `permission` naming | **`permissions`** (plural) everywhere — GET response and POST/PUT request body both use this key | [§7.11](#sec-7-11) |
| 9 | `STATUS` vs `status` casing | **`status`**, lowercase, everywhere — matches the majority of endpoints already | [§7.19](#sec-7-19) |
| 10 | `account_action_mgmt.data` field type | **Real JSON object**, not a stringified Python `repr()` — front will `JSON.parse()` or expect a native object, either way it must be valid JSON | [§7.16](#sec-7-16) |
| 11 | `"susccess"` typo | **Fix to `"success"`** — front should not need to special-case a misspelling | [§7.22](#sec-7-22) |
| 12 | `annoncements` typo | **Fix to `announcements`** | [§7.23](#sec-7-23) |
| 13 | GROUP_MGMT PATCH payload | **Accept `sayeh_profiles`** (or similarly renamed field), not `sayeh_accounts` — matches confirmed [§9.1](#sec-9-1) profile-only group membership | [§7.9](#sec-7-9) |

**Not decided here, still needs backend/architect input:** [§9.2](#sec-9-2) (role/permission vs access-policy/condition interaction) — this is an architecture question, not a frontend preference, needs a real discussion before front builds any policy-editing UI.



<a id="sec-10"></a>
## 10. Changelog (this verification pass)

- Fixed Base URL double-`/sayeh` prefix bug
- Renamed `LOGOUT` → `OIDC_CREDENTIAL` in [§5](#sec-5) table (code didn't match actual behavior)
- Downgraded status on 4 endpoints from DONE to PARTIAL where body/params still unconfirmed (REGISTER_USER, SEND_OTP, VALIDATE_OTP, USER_CREDENTIAL_MANAGEMENT)
- Flagged 6 endpoints as backend TODO (currently 500 in deployment, contract requires 200) — tracked in [§11](#sec-11), not treated as spec ambiguity
- Restructured flat `## 1.1`–`## 5.2` headers (wrong heading level, same as top nav) into nested `### 7.x` under one `## 7` parent
- Surfaced GROUP_MGMT vs PROFILE_GROUPS model conflict as top-priority blocking decision ([§9.1](#sec-9-1)) — this affects whole permission architecture, not cosmetic
- Surfaced role/permission vs access-policy/condition overlap question ([§9.2](#sec-9-2))
- Catalogued smaller naming/typo issues ([§9.3](#sec-9-3)) separately so they don't get lost among bigger conflicts

---

<a id="sec-11"></a>
## 11. Backend Implementation Checklist (contract requires 200 + shape below for all)

This is not a list of "known limitations front has to work around" — every endpoint in this doc is required to return the documented shape at `200`. Below is simply the punch list of what's not there yet in the current deployment, for backend to track and close out. Front should build against the contract, not against current live behavior.

- 6 manage endpoints currently return `500` instead of the documented `200` shape: `group_mgmt`, `role_mgmt`, `permission_mgmt`, `protected_resource_mgmt`, `access_policy_mgmt`, `subcatalogfield_mgmt` — `{"detail": "خطای داخلی سرور رخ داده است."}`. Contracted shapes confirmed from other test env, re-verify against this deployment once fixed
- `INITIAL_CONFIGS` status typo `"susccess"` — fix target: `"success"` ([§9.4](#sec-9-4)#11)
- `account_action_mgmt` `data` field is Python-repr string, not JSON — fix target: real JSON object ([§9.4](#sec-9-4)#10)
- `SAYEH_DASHBOARD_OVERVIEW` field typo `annoncements` — fix target: `announcements` ([§9.4](#sec-9-4)#12)
- `ROLE_MGMT` key naming inconsistency (`permissions` vs `permission`) — fix target: `permissions` everywhere ([§9.4](#sec-9-4)#8)
- `CAS_AUDIT_LOG_AGGRS` key casing inconsistency (`STATUS` vs `status`) — fix target: lowercase `status` ([§9.4](#sec-9-4)#9)
- `GROUP_MGMT` PATCH takes `sayeh_accounts`, contradicts confirmed profile-only group model — fix target: `sayeh_profiles` ([§9.4](#sec-9-4)#13)
- `SEND_OTP` returned `401` in testing — fix target: public, no auth required ([§9.4](#sec-9-4)#6)
- `VALIDATE_OTP` uses GET with params in query — fix target: POST with body ([§9.4](#sec-9-4)#7)
- `LOGOUT` path/name mismatch — resolved by rename in this pass (doc-only fix), was never a logout, always OIDC config fetch, no backend change needed here

---

<a id="sec-12"></a>
## 12. Permission Model (Design Note) — [§9.1](#sec-9-1) confirmed, [§9.2](#sec-9-2) still open

**Confirmed (2026-07-20, group-membership resolved 2026-07-22):**
- Account ↔ Identity: 1:1
- Account → Profiles: 1:N
- Profile = permission boundary — group membership confirmed profile-only ([§9.1](#sec-9-1)), account has no group/role fields
- Role assignment: direct ([§6.4](#profile-roles-post)) + via group inheritance ([§6.3](#profile-groups-post))
- Effective permission = union of direct roles + all inherited roles

Still open: [§9.2](#sec-9-2) (role/permission vs access-policy/condition interaction) — not part of this resolution.
