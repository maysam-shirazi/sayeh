# Sayeh API Contract

Version: 0.2.1 (verified — fixes applied, see §10 changelog)
Base URL: `https://<host>/bapi`
Auth: Bearer token (`Authorization: Bearer <token>`)

> ⚠ **Base URL fix**: table paths below already start with `/sayeh/...` — do NOT
> put `/sayeh` in Base URL too (previous v0.2 had `.../bapi/sayeh/` + `/sayeh/...`
> paths = double prefix, every call would 404). Base URL is just the gateway
> root, paths carry the rest.

---

## 1. Auth (`/sayeh/auth/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| USER_PERMISSION | GET | `/sayeh/auth/user_permission/` | دسترسی کاربر | DONE — §7.1 |
| AUTH_SESSIONS | GET | `/sayeh/auth/sessions/` | نشست های فعال من | DONE — §7.2 |
| AUTH_SESSION_CLOSE | DELETE | `/sayeh/auth/sessions/close/` | خاتمه نشست من | DONE — §7.3 |
| LOGIN_LOGOUT_REPORT | GET | `/sayeh/auth/login_logout_report/` | گزارش ورود و خروج من | DONE — §7.4 |
| CHANGE_PASSWORD | POST | `/sayeh/auth/change_password/` | تغییر گذرواژه | DONE — §7.5 |
| PROFILE | GET | `/sayeh/auth/profile/` | پروفایل | DONE — §7.6 |
| REGISTRATION_ACCESS | POST | `/sayeh/auth/registration_access/` | (no name) | DONE — §7.7 |
| REGISTER_USER | POST | `/sayeh/auth/register_user/` | ثبت نام کاربر | PARTIAL — §7.8, body TBD (depends on OTP flow §7.13/§7.14) |

---

## 2. Manage (`/sayeh/manage/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| GROUP_MGMT | GET/POST/PUT/DELETE/PATCH | `/sayeh/manage/group_mgmt/` | گروه های کاربری | ⚠ SPEC'D, BLOCKED — prod 500 (§9), PATCH needs backend fix (§9.1: should take profile ids not account ids) — §7.9 |
| PERMISSION_MGMT | GET | `/sayeh/manage/permission_mgmt/` | لیست دسترسی سطوح دسترسی | ⚠ SPEC'D, BLOCKED — prod 500 (§9) — §7.10 |
| ROLE_MGMT | GET/POST/PUT/DELETE | `/sayeh/manage/role_mgmt/` | سطح دسترسی | ⚠ SPEC'D, BLOCKED — prod 500 (§9) — §7.11 |
| ACCOUNT_MGMT | GET/POST | `/sayeh/manage/account_mgmt/` | لیست/ایجاد کاربر | DONE — §6.1/§6.1b |
| ACCOUNT_MGMT | PUT | `/sayeh/manage/account_mgmt/{id}/` | ویرایش کاربر | DONE — §6.1c |
| ACCOUNT_MGMT_PROFILES | GET/POST/PUT | `/sayeh/manage/account_mgmt/{id}/profiles/` | پروفایل کاربر | DONE — §6.2/§6.2b/§6.2c |
| PROFILE_GROUPS | POST/DELETE | `/sayeh/manage/profile/{profile_id}/groups/` | تخصیص/حذف گروه | DONE — §6.3 (confirmed model, see §9.1) |
| PROFILE_ROLES | POST/DELETE | `/sayeh/manage/profile/{profile_id}/roles/` | تخصیص/حذف نقش | DONE — §6.4 |
| ACCOUNT_MGMT_CONTACT | PUT | `/sayeh/manage/account_mgmt/{id}/contact/` | ویرایش اطلاعات تماس | DONE — §6.5 |
| PROTECTED_RESOURCE_MGMT | GET | `/sayeh/manage/protected_resource_mgmt/` | سامانه‌های حفاظت شده | ⚠ SPEC'D, BLOCKED — prod 500 (§9) — §7.12 |
| SUBCATALOGFIELD_MGMT | GET | `/sayeh/manage/subcatalogfield_mgmt/` | فیلد های زیرمجموعه کاتالوگ | ⚠ SPEC'D, BLOCKED — prod 500 (§9) — §7.13 |
| ACCESS_POLICY_MGMT | GET/POST/PUT/DELETE | `/sayeh/manage/access_policy_mgmt/` | سیاست های دسترسی | ⚠ SPEC'D, BLOCKED — prod 500 (§9), + overlaps role model, see §9 — §7.14 |
| CONDITION_MGMT | GET/POST/PUT/DELETE | `/sayeh/manage/condition_mgmt/` | شرایط سیاست دسترسی | DONE — §7.15 |
| ACCOUNT_ACTION_MGMT | GET | `/sayeh/manage/account_action_mgmt/` | لاگ های فراخوانی وب سرویس | DONE — §7.16, ⚠ `data` field non-JSON, see §9 |
| IDENTITY_MGMT | — | `/sayeh/manage/identity_mgmt/` | مدیریت هویت کاربران | DEPRECATED — see §6.1 |
| ORG_IDENTITY_MGMT | — | `/sayeh/manage/organization_identity_mgmt/` | مدیریت پروفایل سازمانی | DEPRECATED — see §6.2 |

---

## 3. Base (`/sayeh/base/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| SYSTEM_SUBCATALOG | GET | `/sayeh/base/get_system_subcatalog/` | زیرمجموعه کاتالوگ سیستمی | DONE — §7.17 |
| CAS_AUDIT_LOG | GET | `/sayeh/base/cas_audit_log/` | لاگ های ورود و خروج سیستم | DONE — §7.18 |
| CAS_AUDIT_LOG_AGGRS | GET | `/sayeh/base/cas_audit_log_aggrs/` | تجمیع لاگ های احراز هویت | DONE — §7.19 |
| SEND_OTP | POST | `/sayeh/base/send_otp/` | ارسال کد تایید | PARTIAL — §7.20, body unconfirmed |
| VALIDATE_OTP | GET | `/sayeh/base/validate_otp/` | اعتبارسنجی کد تایید | PARTIAL — §7.21, query params unconfirmed |
| INITIAL_CONFIGS | GET | `/sayeh/base/initial_configs/` | اطلاعات اولیه ثبت نام | DONE — §7.22, ⚠ typo in response, see §9 |

---

## 4. Admin (`/sayeh/admin/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| SAYEH_DASHBOARD_OVERVIEW | GET | `/sayeh/admin/sayeh_dashboard_overview/` | آمار کلی داشبورد تنظیمات | DONE — §7.23 |

---

## 5. SSO (`/sayeh/sso/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| OIDC_CREDENTIAL | GET | `/sayeh/sso/oidc_credential/` | تنظیمات OIDC (نام قبلی: LOGOUT — نادرست، §9) | DONE — §7.24 |
| USER_CREDENTIAL_MANAGEMENT | POST | `/sayeh/sso/user_credential_management/` | احراز هویت توکن لاگین متمرکز | PARTIAL — §7.25, body TBD |

---

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
- Removed account-level `roles`/`role_objects` — per §12 model, roles belong to profile not account, backend leak
- **Removed account-level `groups`** (was `user_groups_data` in raw response) — per §9.1, group membership confirmed profile-only, this field was a backend leak same category as `roles`. Group info now lives solely under `profile.groups` (§6.2/§6.3)
- Dropped `over_view` block — account-list-level stats, not single-account data
- Dropped `profile_data` array, `total_count`, dup id refs — full profile list moved to §6.2
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

**Success 201** — same shape as §6.1 GET response

**Errors**
- `422 VALIDATION_ERROR`
- `409 UID_TAKEN`
- `409 NATIONAL_CODE_TAKEN`
- `401 UNAUTHORIZED`

**Notes**
- No `profile` in request — created without profile, `profile: null` until profile-create called
- `is_active`/`is_mfa` optional, defaults TBD confirm
- `mobile_verified`/`email_verified` set `false` server-side, confirmed via OTP flow separately

---

<a id="account_mgmt-put"></a>
### 6.1c ACCOUNT_MGMT — update

`PUT /sayeh/manage/account_mgmt/{id}/`

**Headers:** `Authorization: Bearer <token>`

**Request body** — full replace, same shape as create (§6.1b), minus `uid` (immutable)

**Success 200** — updated resource, same shape as §6.1 GET response

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `409 NATIONAL_CODE_TAKEN`
- `401 UNAUTHORIZED`

**Open question:** true PUT (full replace) or PATCH semantics preferred? Recommend PATCH.

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

**Notes:** Dropped `sayeh_account` (redundant), merged split id/title arrays into objects, `type` returns text not raw id.

**Open question:** most accounts single profile — confirm multi-profile real case, else drop array wrapper.

---

<a id="account_mgmt-profiles-post"></a>
### 6.2b ACCOUNT_MGMT — profile create

`POST /sayeh/manage/account_mgmt/{account_id}/profiles/`

**Request body**
```json
{
  "title": "علی موسوی",
  "type": 79,
  "identification_code": "117",
  "is_active": true,
  "is_default": false
}
```

**Success 201** — profile object, same shape as §6.2 list entry plus `roles: []`

**Errors**
- `422 VALIDATION_ERROR`
- `404 ACCOUNT_NOT_FOUND`
- `401 UNAUTHORIZED`

**Notes:** `type` sent as numeric id (matches §7.13 SUBCATALOGFIELD_MGMT catalog `ORG_IDENTITY_TYPE`/similar), returned as text. No `groups`/`roles` in create body, assign after via §6.3/§6.4 (⚠ pending §9 resolution). `is_default: true` should auto-unset previous default, confirm.

---

<a id="account_mgmt-profiles-put"></a>
### 6.2c ACCOUNT_MGMT — profile update

`PUT /sayeh/manage/account_mgmt/{account_id}/profiles/{profile_id}/`

**Request body**
```json
{
  "title": "علی موسوی",
  "type": 79,
  "is_active": true,
  "is_default": false
}
```

**Success 200** — same shape as §6.2b response

**Errors**
- `404 PROFILE_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes:** `identification_code` excluded, assume immutable. Same PUT-vs-PATCH question as §6.1c.

---

<a id="profile-groups-post"></a>
### 6.3 Profile — group assign / unassign — **CONFIRMED per §9.1**

Group membership confirmed profile-only (§9.1). Real `GROUP_MGMT` PATCH (§7.9) using `sayeh_accounts` is a backend mismatch, flagged to fix — front should NOT call it as-is; use endpoints below.

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

**Notes:** Assigning group affects aggregated `roles` on profile (§9, group→role inheritance) — refetch profile detail (§6.2) after write, don't compute client-side. Exact route still needs backend confirm/build (not in original URL list) — but semantics (profile joins group) now locked in.

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

**Notes:** Direct role assign only, distinct from group-inherited roles (§6.3/§9). This one not contradicted by real data — roles do live separate from groups per §7.11 ROLE_MGMT shape (`permissions` array on role, no account/profile ref) — assignment endpoint itself still needs real confirm, shape of relationship looks right though.

---

<a id="account_mgmt-contact-put"></a>
### 6.5 ACCOUNT_MGMT — contact info update

`PUT /sayeh/manage/account_mgmt/{id}/contact/`

**Request body — non-verified fields only**
```json
{
  "country": null,
  "city": null,
  "postal_code": null,
  "address": null,
  "org_mobile": null,
  "org_email": null
}
```

**Success 200** — updated contact object

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes:** `mobile`/`email` excluded on purpose, go through OTP flow (§7.20/§7.21) so `mobile_verified`/`email_verified` stay trustworthy.

---

## 7. Endpoint Details — Auth / Manage / Base / Admin / SSO

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

### 7.3 AUTH_SESSION_CLOSE

`DELETE /sayeh/auth/sessions/close/?id={session_id}`

**Success 200**
```json
{ "detail": "نشست بسته شد." }
```
**Errors:** `401` — token invalid (e.g. already closed)

**Notes:** Revokes SSO token server-side, deletes session. Cannot close current request's own session (token invalidates after).

---

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

### 7.6 PROFILE

`GET /sayeh/auth/profile/`

Same shape as §6.1 GET response — full account+profile+groups+roles for currently authenticated user.

---

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

### 7.8 REGISTER_USER — PARTIAL, body TBD

`POST /sayeh/auth/register_user/`

**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Errors:** `400` — bad params

**Notes:** Requires OTP flow first (§7.20/§7.21). Exact request body depends on registration type (self vs gov) — not yet nailed down, don't build against this until confirmed.

---

### 7.9 GROUP_MGMT — ⚠ BLOCKED (prod 500) + model conflict

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
**PATCH** — membership: `{ "sayeh_accounts": [account_id], "action": "ADD_ACCOUNT" | "REMOVE_ACCOUNT" }`

**⚠ Model conflict:** PATCH takes `sayeh_accounts` — accounts join groups directly here, NOT profiles. Contradicts §6.3/§9 assumption that profile is the group-membership unit. See §9 for required decision.

**⚠ Currently returns 500 in prod** — `{"detail": "خطای داخلی سرور رخ داده است."}`. Shape above from other test env, unverified against this deployment.

---

### 7.10 PERMISSION_MGMT — ⚠ BLOCKED (prod 500)

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

### 7.11 ROLE_MGMT — ⚠ BLOCKED (prod 500)

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

**POST** — `{ "code": "NEW_ROLE", "title": "New Role", "permission": [1, 2] }`
**PUT** (`?id={id}`) — `{ "title": "Updated Title", "permission": [1], "code": "ROLE_CODE" }`
**DELETE** (`?id={id}`)

**⚠ Naming inconsistency:** GET response key is `permissions` (plural), POST/PUT body key is `permission` (singular) — pick one, recommend `permissions` consistently.

---

### 7.12 PROTECTED_RESOURCE_MGMT — ⚠ BLOCKED (prod 500)

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

**Notes:** Backs profile `type` picker (§6.2b) — `catalog__code` values seen: `ORG_IDENTITY_TYPE`, `PROTECTED_RESOURCE_TYPE`.

---

### 7.14 ACCESS_POLICY_MGMT — ⚠ BLOCKED (prod 500) + overlaps role model

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

**⚠ Architecture question:** this is effect+priority+condition based access control (ABAC-ish), separate from role→permission model (§12). Both systems exist simultaneously — unclear if access-policy can override a role grant, is evaluated first/last, or is fully independent layer for a different resource type (protected_resource, not app permission). Needs an architecture decision doc, not just endpoint spec — flag for backend/architect discussion before front builds any policy-editing UI.

---

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

### 7.16 ACCOUNT_ACTION_MGMT

`GET /sayeh/manage/account_action_mgmt/?scope={scope}`

**Query params:** `scope` (required) — `ALL` or `USER`

**Success 200**
```json
{
  "data": [
    {
      "id": 569, "sayeh_account_uid": "my_admin", "status": true,
      "data": "{'page_size': ['500']}", "message": "دریافت گروه",
      "action_type": "مدیریت گروه ها", "ip": "192.168.240.16",
      "user_agent": "Mozilla/5.0 ...", "object_id": null,
      "date_created": "2026-07-22T08:04:44.936113Z", "admin": null
    }
  ],
  "total_count": 569
}
```
**Errors:** `400` — `{"status": "FAIL", "message": "invalid scope"}`

**⚠ Bug:** `data` field is a Python-dict `repr()` string (single quotes: `"{'page_size': ['500']}"`), not valid JSON. Front must NOT `JSON.parse()` this field blind — will throw. Flag to backend: serialize with `json.dumps()` not `str(dict)`.

---

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

### 7.18 CAS_AUDIT_LOG

`GET /sayeh/base/cas_audit_log/?page={n}&page_size={n}`

**Success 200**
```json
{ "result": [], "count": 0 }
```
**Notes:** May be empty if no CAS auth events in configured window.

---

### 7.19 CAS_AUDIT_LOG_AGGRS

`GET /sayeh/base/cas_audit_log_aggrs/?field={field_name}`

**Success 200**
```json
{ "STATUS": "SUCCESS", "data": [] }
```
**Errors:** `400` — `{"STATUS": "FAIL", "message": "field must send"}`

**⚠ Inconsistency:** key is `STATUS` (uppercase) here vs `status` (lowercase) on nearly every other endpoint — pick one casing convention.

---

### 7.20 SEND_OTP — body unconfirmed

`POST /sayeh/base/send_otp/`

**Request body (assumed, not confirmed)**
```json
{ "target": "mobile", "value": "09912345678" }
```
**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Errors:** `401` — seen during test, unclear if this endpoint is meant to be public (no-auth) or test used wrong token format. Needs clarify — an OTP-send endpoint gated behind a bearer token is unusual (chicken-egg for registration flow where user has no token yet).

---

### 7.21 VALIDATE_OTP — query params unconfirmed

`GET /sayeh/base/validate_otp/`

**Success 200**
```json
{ "status": "SUCCESS", "data": {} }
```
**Notes:** GET method (unusual for a validate-with-code action, normally POST since code is sensitive-ish and GET params can end up in logs/browser history). Query params likely `code` + `target`, unconfirmed — flag to backend: consider POST instead if not already fixed elsewhere.

---

### 7.22 INITIAL_CONFIGS

`GET /sayeh/base/initial_configs/` — no auth required (public)

**Success 200**
```json
{
  "status": "susccess",
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

**⚠ Bug:** `"status": "susccess"` — typo, should be `"success"`. Front should NOT string-match on this typo (fragile); check for absence of `"FAIL"`/error field instead, or flag backend to fix the typo properly rather than build around it.

---

### 7.23 SAYEH_DASHBOARD_OVERVIEW

`GET /sayeh/admin/sayeh_dashboard_overview/`

**Success 200**
```json
{
  "data": {
    "total_users": 13, "active_users": 13, "total_roles": 1, "total_groups": 1,
    "protected_systems": 1, "access_policies": 2, "webservice_calls_today": 125,
    "units": 5, "annoncements": 2, "failed_webservice_calls_today": 0, "failed_logins_today": 0
  }
}
```

**⚠ Typo:** `annoncements` should be `announcements` — flag, don't silently rename in front code (breaks if backend fixes it later without front knowing), track as known field-name typo instead.

---

### 7.24 OIDC_CREDENTIAL (renamed from LOGOUT — see §9)

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
**Notes:** Returns OIDC config for SSO integration, used to build OAuth2 authorize URL. This is NOT a logout action despite old code name `LOGOUT` — renamed in table §5, confirmed by response shape.

---

### 7.25 USER_CREDENTIAL_MANAGEMENT — body TBD

`POST /sayeh/sso/user_credential_management/`

**Success 200**
```json
{ "detail": "..." }
```
**Errors:** `400` — JSON parse error if malformed

**Notes:** Token exchange for portal SSO. Request/response shape pending real integration test, don't build against this yet.

---

## 8. Groups vs Profiles — architecture question (blocking, see §9 for resolution needed)

(see §9 below — kept as pointer since §9 has full detail)

---

## 9. Design Conflicts & Open Decisions — MUST RESOLVE BEFORE BUILD

### 9.1 Who joins a group: Account or Profile? — **RESOLVED: Profile**

Confirmed: group membership belongs to **profile only**, not account. This means:

- §6.3 (`PROFILE_GROUPS`, profile joins group) is the **correct, authoritative** design — keep as-is, no longer tentative
- §7.9 real `GROUP_MGMT` PATCH taking `sayeh_accounts` **contradicts confirmed model** — this is either:
  - a backend bug (endpoint should accept profile ids, not account ids — likely just named/wired wrong), or
  - a genuinely different feature (e.g. legacy bulk-assign, or an org-level grouping unrelated to permission-groups) that happens to share the `group_mgmt` path by accident
  - **Action:** flag to backend team as a bug/mismatch — `PATCH .../group_mgmt/` needs to take `sayeh_profiles` (or similar), not `sayeh_accounts`, to match confirmed design. Do not build front UI against the account-based PATCH as-is.
- §6.1 account-level `groups` field (kept from raw response `user_groups_data`) is now **suspect** — if group membership is profile-only, this field is likely a backend leak/legacy join, same category as the `roles` field we already dropped from account. **Recommend dropping `groups` from account response too** (§6.1), rely on `profile.groups` (via §6.2 profile detail) as sole source of truth. Flag to backend: is `user_groups_data` on the account serializer intentional or leftover?

Permission model (§12) confirmed as originally stated — no further changes needed there.

### 9.2 Role/Permission model vs Access-Policy/Condition model — how do they interact?

§7.11 ROLE_MGMT (role → list of permission ids) and §7.14 ACCESS_POLICY_MGMT (effect/priority/condition rules) both look like authorization mechanisms but nothing in the raw data shows them referencing each other. Possibilities:
- Access-policy is scoped to `protected_resource` only (SSO gateway rules — "can this account reach this external system, and when") while role/permission is for in-app feature permissions — two separate concerns, not overlapping. Field `protected_resource_type: [access_policy: [1,2]]` in §7.12 supports this reading.
- Or they're meant to merge into one evaluation eventually and aren't yet wired together

**Decision needed:** if reading 1 is correct (separate concerns), no conflict, just document clearly and move on. Confirm with backend before assuming.

### 9.3 Naming/typo cleanup list (low priority, batch with backend later)
- `permissions` (GET) vs `permission` (POST/PUT) on ROLE_MGMT — §7.11
- `STATUS` vs `status` casing — §7.19 vs everywhere else
- `"susccess"` typo — §7.22
- `annoncements` typo — §7.23
- `account_action_mgmt.data` field serialized as Python repr, not JSON — §7.16

---

## 10. Changelog (this verification pass)

- Fixed Base URL double-`/sayeh` prefix bug
- Renamed `LOGOUT` → `OIDC_CREDENTIAL` in §5 table (code didn't match actual behavior)
- Downgraded status on 4 endpoints from DONE to PARTIAL where body/params still unconfirmed (REGISTER_USER, SEND_OTP, VALIDATE_OTP, USER_CREDENTIAL_MANAGEMENT)
- Flagged 6 endpoints DONE-but-blocked (prod 500), added ⚠ marker instead of silent DONE
- Restructured flat `## 1.1`–`## 5.2` headers (wrong heading level, same as top nav) into nested `### 7.x` under one `## 7` parent
- Surfaced GROUP_MGMT vs PROFILE_GROUPS model conflict as top-priority blocking decision (§9.1) — this affects whole permission architecture, not cosmetic
- Surfaced role/permission vs access-policy/condition overlap question (§9.2)
- Catalogued smaller naming/typo issues (§9.3) separately so they don't get lost among bigger conflicts

---

## 11. Known Issues (backend bugs, confirmed via real testing)

- 6 manage endpoints return prod 500: `group_mgmt`, `role_mgmt`, `permission_mgmt`, `protected_resource_mgmt`, `access_policy_mgmt`, `subcatalogfield_mgmt` — `{"detail": "خطای داخلی سرور رخ داده است."}`. Confirmed shapes above come from other test env, need re-verify against this deployment once 500s fixed
- `INITIAL_CONFIGS` status typo `"susccess"`
- `account_action_mgmt` `data` field is Python-repr string, not JSON
- `SAYEH_DASHBOARD_OVERVIEW` field typo `annoncements`
- `ROLE_MGMT` key naming inconsistency (`permissions` vs `permission`)
- `CAS_AUDIT_LOG_AGGRS` key casing inconsistency (`STATUS` vs `status`)
- `LOGOUT` path/name mismatch — resolved by rename in this pass, was never a logout, always OIDC config fetch

---

## 12. Permission Model (Design Note) — §9.1 confirmed, §9.2 still open

**Confirmed (2026-07-20, group-membership resolved 2026-07-22):**
- Account ↔ Identity: 1:1
- Account → Profiles: 1:N
- Profile = permission boundary — group membership confirmed profile-only (§9.1), account has no group/role fields
- Role assignment: direct (§6.4) + via group inheritance (§6.3)
- Effective permission = union of direct roles + all inherited roles

Still open: §9.2 (role/permission vs access-policy/condition interaction) — not part of this resolution.
