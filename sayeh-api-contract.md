# Sayeh API Contract

Version: 0.1 (draft — methods/payloads TBD, fill placeholders)
Base URL: `https://<host>`
Auth: Bearer token (assume, confirm)

Legend for status column: `TODO` = need method + req/resp body from backend dev.

---

## 1. Auth (`/sayeh/auth/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| USER_PERMISSION | TODO | `/sayeh/auth/user_permission/` | دسترسی کاربر | TODO |
| AUTH_SESSIONS | TODO | `/sayeh/auth/sessions/` | نشست های فعال من | TODO |
| AUTH_SESSION_CLOSE | TODO | `/sayeh/auth/sessions/close/` | خاتمه نشست من | TODO |
| LOGIN_LOGOUT_REPORT | TODO | `/sayeh/auth/login_logout_report/` | گزارش ورود و خروج من | TODO |
| CHANGE_PASSWORD | TODO | `/sayeh/auth/change_password/` | تغییر گذرواژه | TODO |
| PROFILE | TODO | `/sayeh/auth/profile/` | پروفایل | TODO |
| REGISTRATION_ACCESS | TODO | `/sayeh/auth/registration_access/` | (no name) | TODO |
| REGISTER_USER | TODO | `/sayeh/auth/register_user/` | ثبت نام کاربر | TODO |

---

## 2. Manage (`/sayeh/manage/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| GROUP_MGMT | TODO | `/sayeh/manage/group_mgmt/` | گروه های کاربری | TODO |
| PERMISSION_MGMT | TODO | `/sayeh/manage/permission_mgmt/` | لیست دسترسی سطوح دسترسی | TODO |
| ROLE_MGMT | TODO | `/sayeh/manage/role_mgmt/` | سطح دسترسی | TODO |
| [ACCOUNT_MGMT](#account_mgmt-get) | GET | `/sayeh/manage/account_mgmt/?id={id}` | لیست کاربران | DONE — [§6.1](#account_mgmt-get) |
| [ACCOUNT_MGMT](#account_mgmt-post) | POST | `/sayeh/manage/account_mgmt/` | ایجاد کاربر | DONE — [§6.1b](#account_mgmt-post) |
| [ACCOUNT_MGMT](#account_mgmt-put) | PUT | `/sayeh/manage/account_mgmt/{id}/` | ویرایش کاربر | DONE — [§6.1c](#account_mgmt-put) |
| [ACCOUNT_MGMT_PROFILES](#account_mgmt-profiles-get) | GET | `/sayeh/manage/account_mgmt/{id}/profiles/` | لیست پروفایل‌های کاربر | DONE — [§6.2](#account_mgmt-profiles-get) |
| [ACCOUNT_MGMT_PROFILES](#account_mgmt-profiles-post) | POST | `/sayeh/manage/account_mgmt/{account_id}/profiles/` | ایجاد پروفایل | DONE — [§6.2b](#account_mgmt-profiles-post) |
| [ACCOUNT_MGMT_PROFILES](#account_mgmt-profiles-put) | PUT | `/sayeh/manage/account_mgmt/{account_id}/profiles/{profile_id}/` | ویرایش پروفایل | DONE — [§6.2c](#account_mgmt-profiles-put) |
| [PROFILE_GROUPS](#profile-groups-post) | POST/DELETE | `/sayeh/manage/profile/{profile_id}/groups/` | تخصیص/حذف گروه پروفایل | DONE — [§6.3](#profile-groups-post) |
| [PROFILE_ROLES](#profile-roles-post) | POST/DELETE | `/sayeh/manage/profile/{profile_id}/roles/` | تخصیص/حذف نقش مستقیم پروفایل | DONE — [§6.4](#profile-roles-post) |
| [ACCOUNT_MGMT_CONTACT](#account_mgmt-contact-put) | PUT | `/sayeh/manage/account_mgmt/{id}/contact/` | ویرایش اطلاعات تماس | DONE — [§6.5](#account_mgmt-contact-put) |
| IDENTITY_MGMT | — | `/sayeh/manage/identity_mgmt/` | مدیریت هویت کاربران | DEPRECATED — see §6.1 |
| ORG_IDENTITY_MGMT | — | `/sayeh/manage/organization_identity_mgmt/` | مدیریت پروفایل سازمانی | DEPRECATED — see §6.2 |
| PROTECTED_RESOURCE_MGMT | TODO | `/sayeh/manage/protected_resource_mgmt/` | سامانه‌های حفاظت شده | TODO |
| SUBCATALOGFIELD_MGMT | TODO | `/sayeh/manage/subcatalogfield_mgmt/` | فیلد های زیرمجموعه کاتالوگ | TODO |
| ACCESS_POLICY_MGMT | TODO | `/sayeh/manage/access_policy_mgmt/` | سیاست های دسترسی | TODO |
| CONDITION_MGMT | TODO | `/sayeh/manage/condition_mgmt/` | شرایط سیاست دسترسی | TODO |
| ACCOUNT_ACTION_MGMT | TODO | `/sayeh/manage/account_action_mgmt/` | لاگ های فراخوانی وب سرویس | TODO |

---

## 3. Base (`/sayeh/base/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| SYSTEM_SUBCATALOG | TODO | `/sayeh/base/get_system_subcatalog/` | زیرمجموعه کاتالوگ سیستمی | TODO |
| CAS_AUDIT_LOG | TODO | `/sayeh/base/cas_audit_log/` | لاگ های ورود و خروج سیستم | TODO |
| CAS_AUDIT_LOG_AGGRS | TODO | `/sayeh/base/cas_audit_log_aggrs/` | تجمیع لاگ های احراز هویت | TODO |
| SEND_OTP | TODO | `/sayeh/base/send_otp/` | ارسال کد تایید | TODO |
| VALIDATE_OTP | TODO | `/sayeh/base/validate_otp/` | اعتبارسنجی کد تایید | TODO |
| INITIAL_CONFIGS | TODO | `/sayeh/base/initial_configs/` | اطلاعات اولیه ثبت نام | TODO |

---

## 4. Admin (`/sayeh/admin/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| SAYEH_DASHBOARD_OVERVIEW | TODO | `/sayeh/admin/sayeh_dashboard_overview/` | آمار کلی داشبورد تنظیمات | TODO |

---

## 5. SSO (`/sayeh/sso/...`)

| Code | Method | Path | Name (fa) | Status |
|---|---|---|---|---|
| LOGOUT | TODO | `/sayeh/sso/oidc_credential/` | خروج از سامانه | TODO |
| USER_CREDENTIAL_MANAGMENT | TODO | `/sayeh/sso/user_credential_management/` | احراز هویت توکن لاگین متمرکز | TODO |

---

## 6. Endpoint details

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
  "groups": [
    { "id": 1, "title": "کارکنان", "code": "personel Department" }
  ],
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
- Dropped `__` prefix flatten (`contact_info__mobile` → `contact.mobile`) — nest instead, easier for front to consume, matches typical UI form shape
- Top-level `identity` object built from `profiles__identity__*` fields — kept, since identity core to account
- Removed account-level `roles`/`role_objects` entirely — per §9, roles belong to profile not account, this was a backend leak
- Dropped `over_view` block — that's account-list-level stats (active/inactive counts), not single-account data. Move to separate endpoint, e.g. `GET /sayeh/manage/account_mgmt/overview/`, only call when dashboard needs it
- Dropped `profile_data` array, `total_count`, dup `profiles__identity: 11` id ref — full profile list moved to §6.2 (`GET /account_mgmt/{id}/profiles/`), only fetched when profile-switcher opened
- **Added `profile`** — the account's `is_default: true` profile, embedded inline, since front always needs active-profile context (name, type, perms) right when account loads, no reason for second call just for this one. Shape matches one entry from §6.2 profile list, minus `groups`/`units` (front can fetch full profile detail if it opens that specific profile's settings) — but WITH `roles` since that's needed immediately for route-guarding on load
- `profiles__identification_code` duplicate of top-level, kept once

**Open question:** does UI screen for this endpoint also need overview stats + full profile list on same view? If yes, either compose on front from 2-3 calls, or backend gives one combined read-model endpoint (`account_mgmt_detail_view`) built for that screen specifically — recommend NOT reusing raw serializer.

**Edge case:** account with zero profiles (broken state, flagged §7 design risk) — `profile` should be `null`, front must handle "no active profile" state (block login or show setup screen, confirm which).

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

**Success 201** — same shape as §6.1 GET response (includes generated `id`, `identification_code`, `groups: []`, `profile: null`)

**Errors**
- `422 VALIDATION_ERROR` — bad/missing fields, `details` field-map
- `409 UID_TAKEN` — uid already exists
- `409 NATIONAL_CODE_TAKEN` — identity.national_code already exists
- `401 UNAUTHORIZED`

**Notes**
- No `profile` in request — account created without profile, `profile: null` in response until profile added via separate profile-create call (not yet spec'd, TODO)
- `is_active`/`is_mfa` optional, default `true`/`false` if omitted — confirm defaults with backend
- `mobile_verified`/`email_verified` not in request — set `false` server-side on create, confirmed via OTP flow (`SEND_OTP`/`VALIDATE_OTP`) separately

---

<a id="account_mgmt-put"></a>
### 6.1c ACCOUNT_MGMT — update

`PUT /sayeh/manage/account_mgmt/{id}/`

**Headers:** `Authorization: Bearer <token>`

**Path params**
- `id` (int, required) — account id

**Request body** — full replace, same shape as create (§6.1b), minus `uid` (immutable, don't send/accept change)
```json
{
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

**Success 200** — updated resource, same shape as §6.1 GET response

**Errors**
- `404 ACCOUNT_NOT_FOUND` — bad id
- `422 VALIDATION_ERROR`
- `409 NATIONAL_CODE_TAKEN` — if changed to value already used by another account
- `401 UNAUTHORIZED`

**Open question:** true PUT (full replace, all fields required every call) or really want PATCH semantics (partial update, only send changed fields)? Front forms usually partial-save friendlier — recommend PATCH instead of PUT if backend can support, else front must always send full object even for single-field edit (more error-prone, stale-data overwrite risk on concurrent edits).

---

<a id="account_mgmt-profiles-get"></a>
### 6.2 ACCOUNT_MGMT — profiles (new, split off from account detail)

`GET /sayeh/manage/account_mgmt/{id}/profiles/`

**Headers:** `Authorization: Bearer <token>`

**Path params**
- `id` (int, required) — account id

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
- `404 ACCOUNT_NOT_FOUND` — bad id
- `401 UNAUTHORIZED`

**Changes from raw backend response — why**
- Dropped `sayeh_account` — caller already knows id from path, redundant
- Merged `unites_id`/`unites_title` split arrays → `units` (array of objects, empty for now, shape TODO once non-empty example seen)
- Merged `groups_id`/`groups_title` split arrays → `groups: [{id, title}]`
- Replaced raw `type: 79` with `type__title` text only, renamed `type` — flag: if front needs numeric type id too (e.g. picker/select), say so and add `type_id` back
- Kept `attributes` as empty array passthrough, shape unknown, revisit when populated

**Open question:** most accounts have single profile — if always 1, consider drop array wrapper and return object directly instead of `{ "profiles": [...] }`. Confirm with backend if multi-profile per account real case.

---

<a id="account_mgmt-profiles-post"></a>
### 6.2b ACCOUNT_MGMT — profile create

`POST /sayeh/manage/account_mgmt/{account_id}/profiles/`

**Headers:** `Authorization: Bearer <token>`

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

**Success 201**
```json
{
  "id": 13,
  "title": "علی موسوی",
  "is_active": true,
  "is_default": false,
  "type": "پرسنل",
  "identification_code": "117",
  "groups": [],
  "roles": [],
  "units": []
}
```

**Errors**
- `422 VALIDATION_ERROR`
- `404 ACCOUNT_NOT_FOUND` — bad account_id
- `401 UNAUTHORIZED`

**Notes**
- `type` sent as id (numeric) in request, returned as `type` text in response (matches §6.2 GET shape) — front needs a type-picker list, TODO endpoint for that (`SYSTEM_SUBCATALOG`? confirm)
- No `groups`/`roles` in create body — assign after, via §6.3/§6.4 (same reasoning as account create, avoid ambiguous array-diff-on-save)
- `is_default: true` on create — should this auto-unset previous default profile server-side? Assume yes, confirm with backend (front shouldn't have to do two calls to swap default)

---

<a id="account_mgmt-profiles-put"></a>
### 6.2c ACCOUNT_MGMT — profile update

`PUT /sayeh/manage/account_mgmt/{account_id}/profiles/{profile_id}/`

**Headers:** `Authorization: Bearer <token>`

**Request body**
```json
{
  "title": "علی موسوی",
  "type": 79,
  "is_active": true,
  "is_default": false
}
```

**Success 200** — same shape as §6.2b create response

**Errors**
- `404 PROFILE_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes**
- `identification_code` excluded from update body — assume immutable after create, confirm with backend
- Same PUT-vs-PATCH open question as §6.1c applies here too

---

<a id="profile-groups-post"></a>
### 6.3 Profile — group assign / unassign (new)

`POST /sayeh/manage/profile/{profile_id}/groups/`

**Request body**
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
- `409 ALREADY_ASSIGNED` — POST only, group already linked
- `401 UNAUTHORIZED`

**Notes**
- Assigning group here affects aggregated `roles` on profile (per §9, group→role inheritance) — front should refetch profile detail (§6.2) after assign/unassign to get updated aggregate, don't try compute client-side
- Not in original URL list — invented path, confirm actual route with backend or adjust to match `GROUP_MGMT` pattern if it already has member-management sub-route

---

<a id="profile-roles-post"></a>
### 6.4 Profile — direct role assign / unassign (new)

`POST /sayeh/manage/profile/{profile_id}/roles/`

**Request body**
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

**Notes**
- This is **direct** role assign only, distinct from group-inherited roles (§6.3) — matches §9 model (direct + via-group, aggregated)
- Same refetch-after-write note as §6.3 applies

---

<a id="account_mgmt-contact-put"></a>
### 6.5 ACCOUNT_MGMT — contact info update

`PUT /sayeh/manage/account_mgmt/{id}/contact/`

**Headers:** `Authorization: Bearer <token>`

**Request body — non-verified fields only, immediate apply**
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

**Success 200** — updated contact object (same shape as §6.1 `contact`)

**Errors**
- `404 ACCOUNT_NOT_FOUND`
- `422 VALIDATION_ERROR`
- `401 UNAUTHORIZED`

**Notes — mobile/email change excluded from this endpoint on purpose**
- `mobile`/`email` are verified fields (`mobile_verified`/`email_verified` flags) — changing them can't be a plain field-set, must go through OTP flow so verified flag stays trustworthy
- Flow: `POST SEND_OTP` (`/sayeh/base/send_otp/`, body TODO — likely `{target: "mobile"|"email", value: "..."}`, target endpoint still marked TODO in §3, needs full spec) → `POST VALIDATE_OTP` (`/sayeh/base/validate_otp/`, body TODO, likely `{target, value, code}`) → on success, verified field flips true and value applied server-side
- Recommend spec SEND_OTP/VALIDATE_OTP next, since contact-info-change and registration both depend on them

---

## 7. Per-endpoint detail template

**Anchor convention:** before each `###` detail heading, add `<a id="{code_lowercase}-{method_lowercase}"></a>` (e.g. `account_mgmt-get`), then link table row's Status cell to `[§X.X](#anchor-id)`. Keeps links working regardless of renderer's heading-slug rules.

Copy this block per endpoint once method + payload known:

```
<a id="<code_lowercase>-<method_lowercase>"></a>
### <CODE>
`<METHOD> <path>`

**Headers:** Authorization: Bearer <token> (if protected)

**Request body**
```json
{}
```

**Success <status>**
```json
{}
```

**Errors**
- `<status> <ERROR_CODE>` — desc
```

---

## 8. Notes / issues found in source list

- Duplicate `id` values: 9 used twice (`ROLE_MGMT`, `ACCOUNT_MGMT`), fix source
- `ACCOUNT_ACTION_MGMT` has two `verbose_name` keys, second overwrites first — dup key, clean up
- Some entries use `verbose_name`, others `verbose_title` — inconsistent, pick one field name
- Several entries missing `id` field (`USER_PERMISSION`, `CONDITION_MGMT`, `CAS_AUDIT_LOG_AGGRS`, `SAYEH_DASHBOARD_OVERVIEW`, `AUTH_SESSIONS`, `AUTH_SESSION_CLOSE`, `LOGIN_LOGOUT_REPORT`, `SEND_OTP`, `VALIDATE_OTP`, `REGISTER_USER`) — need or not?
- `LOGOUT` path `/sayeh/sso/oidc_credential/` — name says logout but path says credential, confirm correct
- `REGISTRATION_ACCESS` — empty verbose_name, needs label
- **`IDENTITY_MGMT` deprecated** — identity is embedded directly in account (§6.1 `identity` object), no separate identity CRUD needed. If backend still exposes standalone identity table/endpoint internally, that's fine, but front never calls it directly — always through account create/update (§6.1b/§6.1c)
- **`ORG_IDENTITY_MGMT` deprecated** — same concept as profile (§6.2), just named differently in source list ("organization profile" ≈ profile). Consolidated into profile endpoints (§6.2/§6.2b/§6.2c), no separate org-identity spec needed. Confirm with backend this mapping correct before removing route entirely — if org-identity actually has extra fields profile doesn't (e.g. org-specific attrs), may need merge fields into profile shape instead of pure rename

## 9. Permission model — design note

**Confirmed design (2026-07-20):**

- Account ↔ Identity: one identity, account is login/auth record tied to it
- Account → Profiles: one account, multiple profiles (one per context/unit)
- Profile = permission boundary — roles/groups/perms all scoped to profile, NOT account
- Role assignment to profile: two paths
  - **Direct** — role attached straight to profile
  - **Via group** — profile in group, group has role(s), inherited
- Final effective permission = **aggregate** of (direct roles) + (all roles from all groups profile belongs to), deduped/unioned

**Implication for API contract:**
- `roles` field seen on raw account response (top level) is WRONG per this model — roles belong on profile, not account. Flag as bug/legacy leftover, exclude from account detail (§6.1), only appear on profile detail (§6.2)
- Profile detail (§6.2) response should probably expose `roles` (aggregated, computed) separate from `direct_roles` (explicit assign only) — front needs both if UI shows "why does this profile have role X" (direct vs inherited-via-group), otherwise just `roles` enough for simple permission checks
- Need endpoint to fetch effective permission list per profile for front route-guarding, e.g. `GET /sayeh/manage/profile/{id}/permissions/` → flat list of permission codes, cheap to check client-side. TODO — not in original URL list, confirm exists or add

**Open question:** on group deletion or role removed from group, does backend recompute/cache effective perms, or compute on-the-fly every request? Doesn't change contract shape but matters for staleness of any cached `roles` front might store.

---

## 10. Open items — fill before build

- [ ] HTTP method per endpoint (GET/POST/PUT/DELETE)
- [ ] Request body schema per endpoint
- [ ] Response body schema per endpoint
- [ ] Error codes per endpoint
- [ ] Which endpoints public vs protected
