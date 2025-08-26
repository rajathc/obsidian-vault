## **1. Problem Statement**

Users often want to extract actionable insights or summaries from a set of related memories, especially after applying filters (e.g., by domain or date). Currently, there's no contextual way for users to query or summarise multiple memory snippets simultaneously, which limits the utility of Neo's memory intelligence.

## **2. Objective**

Enable users to ask questions or generate summaries from filtered or manually selected memory snippets. This enhances productivity, supports use cases like weekly reporting or client updates, and aligns with Neo's core promise of effortless knowledge recall.

## **3. Success Criteria**

- 90%+ of users who use memory filtering discover the Ask Neo option.
- Time-to-summary or response < 5 seconds.
- < 5% of sessions report irrelevant or inaccurate results.
- 30%+ increase in memory sharing/export actions within 2 weeks of launch.
## **4. Feature Description**
### **4.1 Entry Points**

|Trigger|Description|
|---|---|
|Filtered Memories View|User applies filters (e.g., domain, date) and sees a subset of memories.|
|Manual Multi-Select|User manually selects one or more memories from any view.|
|Selection from Filtered View|User views filtered results and selects a specific subset.|

---

## **5. End-to-End User Flow**

### **Step 1: User Lands on Memory Screen**

- Default view shows recent or chronological memories.
- Filters (Date, Domain, Tags) available at top.

### **Step 2: User Applies Filter or Selects Memories**

- **Option A:** Applies filters — all visible memories are auto-selected.
- **Option B:** Manually selects memories via long-press.
- **Option C:** Selects a subset from an already-filtered screen.

### **Step 3: Trigger — Ask Neo Panel Appears**

- Triggered when 1 or more memories are selected.
- Smooth bottom slide-in animation ensures visibility.

**UI Elements:**

- Text input box: _“Ask Neo about these memories…”_
- Button: **Summarise**
    
- Placeholder button (future use): e.g., **Generate Action Items**
    

### **Step 4: User Interacts with Ask Neo**

- **Option 1: Tap “Summarise”**
    
    - Output: Title, bullet points, context highlights, share/copy options.
        
- **Option 2: Enter Custom Prompt**
    
    - Output: Context-aware, relevant response scoped only to selected memories.
        

### **Step 5: Output Delivery**

- Appears inline inside the Ask Neo panel.
    
- Output can be:
    
    - Shared via system share sheet
        
    - Copied
        
    - Saved/exported to other apps
        

---

## **6. Exit Points**

- User deselects all memories → panel disappears.
    
- User taps close button on panel.
    
- User navigates away or refreshes memory screen.
    

---

## **7. UX/UI Notes**

- AI panel must not obstruct the memory view completely.
    
- Default memory selection when filtered.
    
- Loading spinner and error state for AI response.
    
- Inline “Powered by Neo” badge for branding.
    

---

## **8. Example Scenario**

**User:** Ramya  
**Context:** Filters “Sales Calls” in last 7 days.  
**Action:** Selects all > taps “Summarise”.  
**Output:**

- Key client concerns
    
- Committed follow-ups
    
- Sales trend summary  
    **Next:** Copies this for her weekly report.

