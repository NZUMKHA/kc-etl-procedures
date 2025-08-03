
# 🎓 [stage].[spTransform_dimClass]

This stored procedure is part of the King's College Data Warehouse ETL pipeline. It is responsible for transforming class data extracted from Synergetic into the `Transform_dimClass` table, used for academic reporting, student tracking, and Power BI analytics.

---

## 📋 Purpose

- Populate the `[stage].[Transform_dimClass]` table with enriched class metadata.
- Apply classification rules for:
  - **Department** (e.g., English, Mathematics, Science)
  - **Pathway** (e.g., CIE, NCEA, Junior, Other)
  - **QualificationType** (e.g., NCEA Level 1/2/3, AS Level, A Level, IGCSE)
  - **Syllabus Codes** from manual mappings
- Normalize subject names into `MergedSubject`
- Support analysis and reporting downstream in Power BI and SSAS

---

## 🛠 Key Enhancements (2025)

- Added support for new 2025 class description format:
  - e.g., `"Business Studies - NCEA Level 3"` is now correctly identified as `NCEA Level 3`
- Fixed fallback issue where unknown `QualificationType` caused `Pathway = NULL`
- Ensures all Year 11–13 students are assigned correct academic pathway

---

## 🧪 Test Execution

```sql
EXEC [stage].[spTransform_dimClass] 1, 1, 1, 'Test';
```

---

## 📂 Source Dependencies

- `[stage].[Extract_Synergetic_uvStudentClassesAll]`
- `[stage].[Extract_Synergetic_LearningAreas]`
- `[stage].[ref_uSubjectClassesCIEAttributes]`
- `[stage].[Extract_Synergetic_pvAttendancesAll]`
- `[dds].[vDimFileTerm]`

---

## 📤 Target Table

- `[stage].[Transform_dimClass]`

---

## 📦 Output Columns

- `ClassCode`, `Subject`, `QualificationType`, `Pathway`, `Department`
- `BoardStudiesType`, `AssessmentCode`, `CIESyllabusCode`, `MergedSubject`

---

## 👥 Maintainers

- Original Author: Tim Foote
- Contributors: m.kannangara
- Updated for 2025: [U.Khattak]

---

