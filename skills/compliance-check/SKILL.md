---
name: compliance-check
description: Review vendor document submissions for completeness, calculate completion percentages, and identify missing required items.
---

# Vendor Compliance Completeness Skill

## Objective
Evaluate vendor onboarding submissions against predefined compliance checklists to identify missing required documents, calculate submission completeness, and provide actionable audit results.

---

## Required Inputs
- `vendor_id`: Unique identifier for the vendor (string).
- `vendor_name`: Legal trading name of the vendor (string).
- `required_documents`: Standardized list of mandatory document types (list of strings).
  - Example: `["Certificate of Incorporation", "Tax Compliance Certificate", "Business Permit", "Bank Details Confirmation", "Director Identification"]`
- `submitted_documents`: List of document records submitted by the vendor (list of strings or objects).

---

## Procedure
1. **Load Checklist**: Retrieve the list of mandatory required documents for the vendor category.
2. **Normalize Submission Data**: Standardize submitted document names (trim whitespace, lower/case-fold matching) and deduplicate repeated submissions.
3. **Compare Records**: Check each required document against the deduplicated submitted records.
4. **Identify Gaps**: Compile an explicit list of missing required documents.
5. **Count Submissions**: Count unique submitted required documents ($S$) and total required documents ($R$).
6. **Calculate Percentage**:
   $$\text{Completion Percentage} = \left(\frac{S}{R}\right) \times 100$$
7. **Determine Review Status**:
   - If $\text{Completion Percentage} = 100\% \rightarrow \text{"READY_FOR_HUMAN_EVALUATION"}$
   - If $\text{Completion Percentage} < 100\% \rightarrow \text{"INCOMPLETE_DOCUMENTS_PENDING"}$
8. **Format Structured Result**: Return a structured JSON or Markdown report highlighting missing items and next actions.
9. **Escalate**: Flag all incomplete or ambiguous submissions for human procurement officer follow-up.

---

## Calculation Rules
- **Formula**:
  $$\text{Completeness (\%)} = \left(\frac{\text{Unique Valid Submitted Required Documents}}{\text{Total Required Documents}}\right) \times 100$$
- **Range**: Must strictly resolve to a value between $0.0\%$ and $100.0\%$.
- **Deduplication**: Submitting the same document multiple times (e.g., three copies of "Tax Certificate") counts as exactly 1 valid submission.
- **Extra Documents**: Submitting optional documents not on the required list does not increase the numerator beyond the required count.

---

## Expected Output Format
```json
{
  "vendor_id": "VEND-001",
  "vendor_name": "Alpha Ltd",
  "total_required": 5,
  "submitted_count": 5,
  "completion_percentage": 100.0,
  "missing_documents": [],
  "status": "READY_FOR_HUMAN_EVALUATION",
  "human_review_required": true,
  "notes": "All required documents received. Ready for human compliance officer verification of authenticity."
}
```

---

## Validation Rules
- **Missing Items Must Be Explicit**: Every missing document must be individually named in the output report.
- **Authenticity Disclaimer**: Completeness checking verifies *presence only*, not document authenticity or validity.
- **No Inferred Data**: Missing submissions must never be fabricated, assumed, or imputed.

---

## Boundaries & Restrictions
- **Do Not Approve Vendors**: Never issue final vendor approvals; approval is an exclusive human prerogative.
- **Do Not Bypass Requirements**: Under no circumstance should a vendor with $< 100\%$ completeness be marked as ready for onboarding.
- **Reject Unverified Data**: If document metadata is unreadable, treat the item as unsubmitted and flag for human review.
