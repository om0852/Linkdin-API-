# 📄 LinkedIn API Documentation

**Author:** Om Salunke  
**Date:** August 2025  
**Purpose:** This document explains the LinkedIn REST API calls used, their endpoints, request formats, and sample responses.

---

## 1️⃣ Get Current User Profile
**Endpoint**
```
GET https://api.linkedin.com/v2/me
```
**Headers**
```
Authorization: Bearer {access_token}
LinkedIn-Version: 202505
```
**Description**  
Fetches the authenticated user’s basic profile details.
**Sample Response**
```json
{
    "localizedLastName": "Salunke",
    "profilePicture": {
        "displayImage": "urn:li:digitalmediaAsset:D4D03AQEJb8p-HHmQcA"
    },
    "firstName": {
        "localized": {"en_US": "Om"},
        "preferredLocale": {"country": "US", "language": "en"}
    },
    "vanityName": "om-salunke-81bb63292",
    "lastName": {
        "localized": {"en_US": "Salunke"},
        "preferredLocale": {"country": "US", "language": "en"}
    },
    "localizedHeadline": "Full Stack Web | Blockchain developer",
    "id": "fz4gLtBTn9"
}
```
**Use Case** – Display logged-in user info on a dashboard or profile section.

---

## 2️⃣ Get Creator Post Analytics (Comments Count)
**Endpoint**
```
GET https://api.linkedin.com/rest/memberCreatorPostAnalytics
  ?q=me
  &aggregation=TOTAL
  &queryType=COMMENT
  &dateRange=(start:(day:4,month:5,year:2024),end:(day:6,month:5,year:2025))
```
**Headers**
```
Authorization: Bearer {access_token}
X-Restli-Protocol-Version: 2.0.0
LinkedIn-Version: 202506
```
**Description**  
Retrieves aggregated comment counts on creator posts for a given date range.
**Sample Response**
```json
{
    "paging": {"start": 0, "count": 10, "links": [], "total": 1},
    "elements": [
        {
            "count": 2,
            "dateRange": {},
            "metricType": {
                "com.linkedin.adsexternalapi.memberanalytics.v1.CreatorPostAnalyticsMetricTypeV1": "COMMENT"
            }
        }
    ]
}
```

---

## 3️⃣ Get Total Follower Count (Personal Profile)
**Endpoint**
```
GET https://api.linkedin.com/rest/memberFollowersCount?q=me
```
**Headers**
```
Authorization: Bearer {access_token}
LinkedIn-Version: 202505
```
**Description**  
Fetches the total number of followers for the authenticated member.
**Sample Response**
```json
{
    "paging": {"start": 0, "count": 10, "links": [], "total": 1},
    "elements": [
        {
            "memberFollowersCount": 961
        }
    ]
}
```

---

## 4️⃣ Get Daily Follower Count (Date Range)
**Endpoint**
```
GET https://api.linkedin.com/rest/memberFollowersCount
  ?q=dateRange
  &dateRange=(start:(year:2024,month:5,day:4),end:(year:2024,month:5,day:6))
```
**Headers**
```
Authorization: Bearer {access_token}
LinkedIn-Version: 202505
```
**Description**  
Fetches follower count per day within a specific date range.
**Sample Response**
```json
{
    "paging": {"start": 0, "count": 10, "links": [], "total": 2},
    "elements": [
        {
            "dateRange": {"start": {"month": 5, "year": 2024, "day": 4}, "end": {"month": 5, "year": 2024, "day": 5}},
            "memberFollowersCount": 0
        },
        {
            "dateRange": {"start": {"month": 5, "year": 2024, "day": 5}, "end": {"month": 5, "year": 2024, "day": 6}},
            "memberFollowersCount": 0
        }
    ]
}
```

---

## 5️⃣ Get Organization ACLs (Roles)
**Endpoint**
```
GET https://api.linkedin.com/rest/organizationAcls?q=roleAssignee
```
**Headers**
```
Authorization: Bearer {access_token}
LinkedIn-Version: 202501
X-Restli-Protocol-Version: 2.0.0
```
**Description**  
Fetches organization access control list entries for which the member is a role assignee (e.g., admin).
**Sample Response**
```json
{
    "paging": {"start": 0, "count": 10, "links": []},
    "elements": [
        {
            "roleAssignee": "urn:li:person:fz4gLtBTn9",
            "state": "APPROVED",
            "role": "ADMINISTRATOR",
            "organization": "urn:li:organization:108187115"
        }
    ]
}
```

---

## 6️⃣ Get Organization Follower Statistics
**Endpoint**
```
GET https://api.linkedin.com/rest/organizationalEntityFollowerStatistics
  ?q=organizationalEntity
  &organizationalEntity=urn:li:organization:108187115
```
**Description**  
Retrieves various follower statistics for the given organization.
**Sample Response**
```json
{
    "paging": {"start": 0, "count": 10, "links": []},
    "elements": [
        {
            "followerCountsByAssociationType": [],
            "followerCountsBySeniority": [],
            "followerCountsByIndustry": [],
            "followerCountsByFunction": [],
            "followerCountsByStaffCountRange": [],
            "followerCountsByGeoCountry": [],
            "followerCountsByGeo": [],
            "organizationalEntity": "urn:li:organization:108187115"
        }
    ]
}
```

---

## 📝 Notes
- Replace `{Access_token}` with a valid OAuth 2.0 access token.
- All APIs require proper LinkedIn API permissions.
- Date ranges must follow LinkedIn’s structured parameter format.
