---
applyTo: '**/*.md'
---

# Thailand Travel Project - Markdown Instructions

## Overview
This project contains travel itinerary documents for Thailand. All markdown files must follow these guidelines to ensure images display correctly and content is accurate.

---

## Image Formatting (CRITICAL - NON-NEGOTIABLE)

### Working Format for VS Code Markdown Preview

**USE THIS FORMAT:**
```markdown
![Image Description](https://commons.wikimedia.org/wiki/Special:FilePath/Filename_Here.jpg)
*Caption describing the image*
```

**Example:**
```markdown
![Doi Suthep Temple](https://commons.wikimedia.org/wiki/Special:FilePath/Sunset_doi_suthep_temple.jpg)
*The golden spires of Wat Phra That Doi Suthep at sunset*
```

### Formats That DO NOT Work in VS Code Preview

| Format | Example | Status |
|--------|---------|--------|
| Wikimedia Thumb URLs | `https://upload.wikimedia.org/wikipedia/commons/thumb/...` | ❌ BROKEN |
| Direct upload URLs | `https://upload.wikimedia.org/wikipedia/commons/a/b1/File.jpg` | ❌ BROKEN |
| HTML img tags | `<img src="...">` | ❌ BROKEN |

### Formats That Work

| Format | Example | Status |
|--------|---------|--------|
| Unsplash URLs | `https://images.unsplash.com/photo-...?w=1200&q=80` | ✅ Works |
| Wikimedia Special:FilePath | `https://commons.wikimedia.org/wiki/Special:FilePath/File.jpg` | ✅ Works |

---

## Image Accuracy Requirements (100% NON-NEGOTIABLE)

### CRITICAL: Images MUST Match Captions

Every image embedded in a markdown document **MUST**:

1. **Actually depict the location stated in the caption**
   - If the caption says "Doi Suthep Temple" → the image MUST show Doi Suthep Temple
   - If the caption says "Pai Canyon" → the image MUST show Pai Canyon (NOT a temple, NOT random mountains)
   - Generic stock photos are NOT acceptable

2. **Use verified, geotagged images from Wikimedia Commons**
   - Search Wikimedia Commons categories for each location
   - Verify the image filename matches the location
   - Cross-reference with category listings

3. **Represent the correct season/timeframe when dates are specified**
   - This itinerary is for **April 10 - May 4** (late dry season / early monsoon transition)
   - Thailand in April/May has:
     - Hot, humid weather (30-40°C)
     - Lush GREEN tropical vegetation
     - Clear skies transitioning to occasional rain
   - Images showing the following are **INCORRECT** for April/May:
     - ❌ Snow-capped mountains (impossible in tropical Thailand)
     - ❌ Brown/dry vegetation (wrong season)
     - ❌ Heavy monsoon flooding (too early)
     - ❌ Cool-season foggy mornings (wrong season)

### Verification Checklist Before Adding Any Image

- [ ] Image filename clearly identifies the location
- [ ] Image is from Wikimedia Commons verified category for that location
- [ ] Visual content matches the caption text
- [ ] Seasonal conditions match the trip dates (if applicable)
- [ ] Image uses `Special:FilePath` format (not `upload.wikimedia.org/thumb`)

---

## Wikimedia Commons Image Sourcing Process

### Step 1: Find the Category
Navigate to: `https://commons.wikimedia.org/wiki/Category:[Location_Name]`

Examples:
- Doi Suthep: `https://commons.wikimedia.org/wiki/Category:Doi_Suthep`
- Pai Canyon: `https://commons.wikimedia.org/wiki/Category:Pai_Canyon`
- Phang Nga Bay: `https://commons.wikimedia.org/wiki/Category:Phang_Nga_Bay`
- Khao Sok: `https://commons.wikimedia.org/wiki/Category:Khao_Sok_National_Park`

### Step 2: Select an Appropriate Image
- Review thumbnails in the category
- Choose images with descriptive filenames
- Prefer images that clearly show the landmark/location

### Step 3: Construct the FilePath URL
Take the filename and create:
```
https://commons.wikimedia.org/wiki/Special:FilePath/[Exact_Filename.jpg]
```

---

## URL Encoding Rules (CRITICAL - Root Cause of Broken Images)

The `Special:FilePath` redirect is **filename-sensitive**. VS Code's Markdown parser requires proper URL encoding for special characters.

### Characters That MUST Be URL-Encoded

| Character | Encode As | Example |
|-----------|-----------|---------|
| Space ` ` | `%20` | `Sunrise at lake.jpg` → `Sunrise%20at%20lake.jpg` |
| Comma `,` | `%2C` | `Khao_Sok,_Thailand.jpg` → `Khao_Sok%2C_Thailand.jpg` |

### Encoding Examples

**File with spaces in name:**
```
✅ CORRECT: https://commons.wikimedia.org/wiki/Special:FilePath/Sunrise%20at%20Cheow%20Lan%20lake.jpg
❌ WRONG:   https://commons.wikimedia.org/wiki/Special:FilePath/Sunrise_at_Cheow_Lan_lake.jpg
```

**File with commas in name:**
```
✅ CORRECT: https://commons.wikimedia.org/wiki/Special:FilePath/Khao_Sok%2C_Cheow_Lan_Lake%2C_Thailand.jpg
❌ WRONG:   https://commons.wikimedia.org/wiki/Special:FilePath/Khao_Sok,_Cheow_Lan_Lake,_Thailand.jpg
```

### Best Practice: Choose Simple Filenames

When selecting images from Wikimedia Commons, **prefer images with simple filenames** that use only:
- Letters (a-z, A-Z)
- Numbers (0-9)
- Underscores (_)
- Hyphens (-)
- Dots (.)

Avoid filenames with spaces, commas, parentheses, or special characters when possible.

---

## Location-Specific Image Sources (Verified Working)

| Location | Recommended Wikimedia Category | Example Filename | Encoding Notes |
|----------|-------------------------------|------------------|----------------|
| Bangkok | Category:Bangkok, Category:Grand_Palace_Bangkok | `Grand_Palace_Bangkok.jpg` | Simple name |
| Chiang Mai | Category:Chiang_Mai | `Chiang_Mai_and_Doi_Suthep_Mountain_2017.jpg` | Simple name |
| Doi Suthep | Category:Doi_Suthep | `Sunset_doi_suthep_temple.jpg` | Simple name |
| Pai Canyon | Category:Pai_Canyon | `Pai_Canyon.jpg` | Simple name |
| Songkran | Category:Songkran_in_Thailand | `Songkran_Day_@_Chiangmai_Wall.jpg` | `@` may need encoding |
| Phang Nga Bay | Category:Phang_Nga_Bay | `Phang_Nga_Bay%2C_Thailand.jpg` | **Comma → %2C** |
| James Bond Island | Category:Ko_Tapu | `Ko_Tapu_James_Bond_Island.jpg` | Avoid parentheses |
| Koh Phi Phi | Category:Views_of_Ko_Phi_Phi_Don | `Koh_Phi_Phi_viewpoint_panorama.jpg` | Avoid parentheses |
| Maya Bay | Category:Maya_Bay | `Maya_Bay%2C_Thailand.jpg` | **Comma → %2C** |
| Railay Beach | Category:West_Rai_Leh | `Railay_Beach_Limestone_Cliffs.jpg` | Simple name |
| Khao Sok Lake | Category:Khao_Sok_National_Park | `Sunrise%20at%20Cheow%20Lan%20lake.jpg` | **Spaces → %20** |
| Khao Sok Jungle | Category:Khao_Sok_National_Park | `Khao_Sok%2C_Cheow_Lan_Lake%2C_Thailand.jpg` | **Commas → %2C** |

---

## Common Mistakes to Avoid

### 1. Not URL-Encoding Special Characters (ROOT CAUSE OF BROKEN IMAGES)
❌ **Wrong:** `Special:FilePath/Khao_Sok,_Cheow_Lan_Lake,_Thailand.jpg` (unencoded commas)
✅ **Right:** `Special:FilePath/Khao_Sok%2C_Cheow_Lan_Lake%2C_Thailand.jpg` (encoded commas)

❌ **Wrong:** `Special:FilePath/Sunrise_at_Cheow_Lan_lake.jpg` (underscores where spaces exist)
✅ **Right:** `Special:FilePath/Sunrise%20at%20Cheow%20Lan%20lake.jpg` (actual filename has spaces)

### 2. Using Generic Stock Photos
❌ **Wrong:** Using any "tropical beach" photo for "Railay Beach"
✅ **Right:** Using a photo specifically from Railay with limestone cliffs visible

### 3. Wrong Season Imagery
❌ **Wrong:** Snow-capped mountains for "Pai Valley" in April
✅ **Right:** Lush green tropical mountains for Northern Thailand in hot season

### 3. Mismatched Landmarks
❌ **Wrong:** A temple photo labeled as "Pai Canyon"
✅ **Right:** Red-earth canyon ridges photo for Pai Canyon

### 4. Broken URL Formats
❌ **Wrong:** `https://upload.wikimedia.org/wikipedia/commons/thumb/a/b1/File.jpg/1200px-File.jpg`
✅ **Right:** `https://commons.wikimedia.org/wiki/Special:FilePath/File.jpg`
### 6. Assuming Underscores Replace Spaces
❌ **Wrong:** Assuming `Sunrise_at_lake.jpg` is the same as `Sunrise at lake.jpg`
✅ **Right:** Check the EXACT filename on Wikimedia Commons and URL-encode spaces as `%20`
---

## Currency Display Requirements (MANDATORY)

All costs and prices in the itinerary **MUST** be displayed in both currencies:

### Format
```
[Amount] THB (~£[GBP equivalent])
```

### Exchange Rate
Use approximate rate: **1 GBP = 44 THB** (verify current rate before final editing)

### Examples
| Context | Format |
|---------|--------|
| Single price | `200 THB (~£4.50)` |
| Price range | `500-800 THB (~£11-18)` |
| Daily budget | `2,000 THB (~£45)/day` |
| Per person | `1,500 THB (~£34)/person` |

### Rules
1. THB comes first (local currency), GBP in parentheses
2. GBP uses `~£` prefix to indicate approximation
3. Round GBP to nearest 50p for amounts under £10, nearest £1 for larger amounts
4. Keep the same format throughout the document

---

## Quality Standards Summary

| Requirement | Priority | Notes |
|-------------|----------|-------|
| Image matches caption location | **CRITICAL** | 100% non-negotiable |
| Seasonal accuracy | **HIGH** | Must reflect April/May conditions |
| URL format (Special:FilePath) | **HIGH** | Required for VS Code preview |
| Verified source (Wikimedia Commons) | **HIGH** | Ensures geotagged accuracy |
| Image quality/resolution | Medium | Prefer images >1200px wide |

---

*Last updated: Document creation*
*Applies to: All markdown files in Thailand travel project*
