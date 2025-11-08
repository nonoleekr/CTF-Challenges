# CTF Challenge: Track Down Kuki Godam’s Birthday

## Challenge Description

Determine the birthday of “Kuki Godam” based on clues scattered across social media.  
**Flag format:** `SKR{yyyy_mm_dd}`

---

## Approach & Solution

### 1. Google Search

Searching for “Kuki Godam” landed on a Facebook profile.

### 2. Checking Profile Info

In the *About > Contact and Basic Info* section, the birth year `1997` was listed.

### 3. Analyzing Posts

- One post shares a YouTube video about "top 10 facts about people born on a Saturday", confirming the target day.
- Another post discusses zodiac signs, notably “Scorpio” with a date mention: March 16, 2019. This is likely a distraction, since Scorpio corresponds to late October–November.
- The oldest post is a profile picture upload where "Kuki Godam" comments: `I rate my profile picture 10/25`. This number stands out as a potential clue for month and day.

### 4. Synthesizing Clues

- **Year:** 1997 (from profile)
- **Month/Day:** 10/25 (from comment), corresponding to October 25th.
- Verified that **October 25, 1997** is a Saturday, matching all clues.

### 5. Submitting the Flag

Final flag:  
```
SKR{1997_10_25}
```

---

## Notes

- The zodiac and Saturday clues can be misdirections. The key was the self-commented date "10/25" tied to the birth year.
- Always double-check the day of the week for date-based challenges.
