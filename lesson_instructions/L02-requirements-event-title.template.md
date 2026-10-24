
**Student:** Tamar Faigenboim  
**Date:** 25/10/2026
**Fork URL:**   https://github.com/Binah-CS/event-photo-capstone.git

## 1. Original request (do not reinterpret)

> I entered the wrong event name. I want to be able to change the event name displayed in the client's gallery.

## 2. Current behavior — verified facts

| Claim | Evidence | Verified? |
| --- | --- | --- |
| לכל אירוע יש שדה המייצג את שמו | השדה `title` מוגדר מסוג `string` בתוך `EventRecord`. מקור: `src/domain/types.ts` | כן |
| שם האירוע נכלל בנתוני הגלריה | הפונקציה `getClientGallery` מחזירה את `event.title`. מקור: `src/services/event-service.ts` | לבדיקה אישית |
| לא קיימת פעולה ייעודית לשינוי שם האירוע | לא נמצא נתיב עדכון ב־`src/http/app.ts` או שירות מתאים ב־`src/services/event-service.ts` | לבדיקה אישית |

## 3. Actors / users / use cases / permissions

- **Actors:** צלם ולקוח.
- **Verified:** הצלם מנהל אירועים והלקוח צופה בגלריה ובוחר תמונות.
- **Use case:** תיקון שם שגוי של אירוע קיים.
- **Must clarify:** האם רק הצלם רשאי לשנות את השם, או שגם הלקוח יכול לבצע את השינוי?

## 4. Goal, scope, out of scope

**Goal:** לאפשר תיקון שם אירוע כך שהשם המעודכן יוצג בגלריית הלקוח.

**In scope (provisional):**
- שינוי שם של אירוע קיים.
- הצגת השם המעודכן בגלריית הלקוח.

**Out of scope (provisional):**
- יצירת אירועים חדשים.
- מחיקת אירועים.
- שינוי התמונות המשויכות לאירוע.

**Undecided:**
- האם השם החדש צריך להופיע גם ברשימת האירועים?
- האם ניתן לשנות שם לאחר פרסום הגלריה?
- מהם הכללים לשם אירוע תקין?

## 5. Functional requirements

- **FR-1 (זמני):** משתמש מורשה יוכל לשנות את שמו של אירוע קיים.
- **FR-2 (זמני):** לאחר שינוי מוצלח, השם החדש יוצג בגלריית הלקוח.
- **FR-3 (זמני):** שינוי השם לא ישפיע על התמונות המשויכות לאירוע.
- **FR-4 (מותנה):** המערכת תדחה שם שאינו עומד בכללי התקינות שייקבעו.

## 6. Non-functional requirements / constraints

- **NFR-1:** רק משתמש מורשה יוכל לבצע שינוי שם.
- **NFR-2:** השם המעודכן יוצג בתוך פרק זמן שייקבע.
- **NFR-3:** שינוי השם לא יפגע בגישה לגלריה.

**Constraint:** המערכת שומרת כרגע נתונים בזיכרון, ולא קיימת פעולה ייעודית לשינוי שם אירוע.

## 7. Ten analysis lenses from the preparation assignment

| Term | Question relevant to this change | Answer known? |
| --- | --- | --- |
| Functional requirements | האם השם החדש צריך להתעדכן גם ברשימת האירועים? | לא ידוע |
| Non-functional requirements | האם השם החדש צריך להופיע מיד לאחר השמירה או רק לאחר רענון? | לא ידוע |
| Actors / users | מי רשאי לשנות את שם האירוע — הצלם או גם הלקוח? | לא ידוע |
| Use cases | מה קורה כאשר משתמש מנסה להזין שם לא תקין? | לא ידוע |
| Constraints | האם ניתן לשנות שם גם לאחר פרסום הגלריה? | לא ידוע |
| Assumptions | האם נדרש להוסיף פעולה חדשה ב־API? | הנחה לא מאומתת |
| Acceptance criteria | כיצד נבדוק שהשם החדש מופיע בגלריה? | ראו סעיף 9 |
| Ambiguity | האם השינוי צריך להופיע בכל המקומות שבהם מוצג שם האירוע? | לא ידוע |
| Missing information | האם יש צורך לשמור היסטוריה של שמות קודמים? | לא ידוע |
| Scope | האם המשימה כוללת רק שינוי שם או גם שינויים במסכי הניהול? | לא הוכרע |

## 8. Questions, assumptions, ambiguities

### Five initial questions

1. **Actors / Users:** מי בדיוק רשאי לבצע את עדכון שם האירוע — האם רק הצלם שיצר את האירוע, או שגם הלקוח הצופה בגלריה מורשה לשנותו?
2. **Acceptance Criteria:** כיצד נוודא שהשינוי הצליח — האם השם המעודכן צריך להופיע מיד ללא רענון, או שמספיק שיופיע לאחר רענון הדף?
3. **Constraints:** האם קיימות מגבלות על אורך השם או על תווים מיוחדים, והאם ניתן לשנות את השם גם לאחר פרסום הגלריה?
4. **Missing Information:** האם המערכת צריכה לשמור היסטוריה של שמות קודמים לצורכי מעקב ובקרה?
5. **Scope:** האם המשימה כוללת רק עדכון של שם האירוע, או גם שינויים במסכי הניהול של הצלם?

### Questions and assumptions table

| Question or assumption | Why it matters | Evidence/status | Who decides? |
| --- | --- | --- | --- |
| מי רשאי לשנות את השם? | כדי לקבוע הרשאות | לא ידוע | בעל הדרישה |
| האם השם מתעדכן ללא רענון? | כדי להגדיר התנהגות צפויה | לא ידוע | בעל הדרישה |
| האם מותר לשנות שם לאחר פרסום? | כדי לקבוע מגבלות על הפעולה | לא ידוע | בעל הדרישה |
| האם צריך לשמור היסטוריית שמות? | כדי לקבוע את היקף המשימה | לא ידוע | בעל הדרישה |
| האם צריך לעדכן גם את רשימת האירועים? | כדי לשמור על עקביות | לא ידוע | בעל הדרישה |
| הנחה: נדרשת פעולה חדשה ב־API | כדי לתכנן את יכולת העדכון | לא אומת | צוות הפיתוח לאחר אישור הדרישה |

## 9. Acceptance criteria (provisional)

**AC-1 — Successful rename**

Given אירוע קיים ומשתמש מורשה,  
When המשתמש משנה את שם האירוע לשם תקין,  
Then השם המעודכן מופיע בגלריית הלקוח.

**AC-2 — Unauthorized rename**

Given אירוע קיים ומשתמש שאינו מורשה לערוך אותו,  
When המשתמש מנסה לשנות את שם האירוע,  
Then המערכת דוחה את השינוי ושם האירוע נשאר ללא שינוי.

## 10. Error cases and tests

- **Unknown event:** יש להגדיר כיצד המערכת תגיב לניסיון לשנות שם של אירוע שאינו קיים.
- **Unauthorized requester:** המערכת לא תאפשר את השינוי.
- **Empty title:** יש להחליט אם שם ריק נחשב לא תקין.
- **Existing client gallery after change:** יש לוודא שהגלריה מציגה את השם החדש ושהתמונות לא משתנות.
- **Repeated update:** יש לברר אם ניתן לשנות את שם האירוע מספר פעמים.

## 11. AI checkpoints: understanding / questioning / spec review

**Claim to verify in source:** הפונקציה `getClientGallery` מחזירה את שם האירוע באמצעות `event.title`.

**Source:** `src/services/event-service.ts`

### AI suggestions — for student review

| AI suggestion | Suggested status | Justification | Evidence |
| --- | --- | --- | --- |
| לבדוק האם השם החדש צריך להופיע גם ברשימת האירועים | Essential — מוצע לאימוץ | חשוב למנוע מצב שבו אותו אירוע מוצג בשמות שונים | `listEvents`, `getClientGallery` |
| להוסיף היסטוריה של כל שינויי השמות | Later — מוצע לדחייה | הבקשה המקורית מתייחסת לתיקון שם, ולא לשמירת היסטוריית שינויים | לא נדרש בבקשה |

*התלמידה צריכה לבדוק את ההצעות ולסמן את ההחלטות שקיבלה בפועל.*

## 12. Remaining decisions (do not silently invent answers)

- מי רשאי לשנות את שם האירוע?
- האם ניתן לשנות שם לאחר פרסום הגלריה?
- האם השם צריך להתעדכן גם ברשימת האירועים?
- מהו האורך המותר לשם האירוע?
- האם יש צורך לשמור היסטוריה של שמות קודמים?
- כיצד יש לטפל בניסיון לשנות שם של אירוע שאינו קיים?

## 13. Personal reflection

**One fact discovered through code review:**  
[להשלים לאחר בדיקה אישית בקוד. לדוגמה, אפשר לבדוק כיצד `getClientGallery` מחזירה את שם האירוע.]

**One AI suggestion rejected or postponed, and why:**  
[להשלים לפי החלטת התלמידה. לדוגמה, ניתן לדחות הוספת היסטוריית שמות משום שאינה נדרשת בבקשה המקורית.]