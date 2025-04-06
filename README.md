import com.atlassian.jira.component.ComponentAccessor
import com.atlassian.jira.issue.history.ChangeItemBean

def issueKey = "ABC-123"  // Replace with your issue key
def statusName = "In Review" // Replace with your actual status name

def issueManager = ComponentAccessor.issueManager
def changeHistoryManager = ComponentAccessor.changeHistoryManager

def issue = issueManager.getIssueByCurrentKey(issueKey)

if (!issue) {
    return "Issue not found: $issueKey"
}

// Get all status change items
def statusChanges = changeHistoryManager.getChangeItemsForField(issue, "status")

// Find the most recent transition to "In Review"
def targetTransition = statusChanges.findLast { it.toString == statusName }

if (targetTransition) {
    return "Transition to '$statusName' occurred on: ${targetTransition.created}"
} else {
    return "No transition to '$statusName' found for issue $issueKey"
}

Here’s the updated professional description incorporating the additional details:  

---

**QM KPI Metric Tool** is a Java-based application designed to collect, store, and visualize key quality management metrics across multiple testing platforms. The tool integrates with various systems to provide a comprehensive view of test execution and defect tracking:  

- **Manual Test Execution**: Data is retrieved from **qTest Manager**, offering insights into manual testing efforts.  
- **Defect Tracking**: Defects can be tracked in **qTest Manager and/or JIRA**, depending on the preferences of the test and development teams.  
- **Automated Test Execution**: Metrics are collected through **test automation listeners**, supporting widely used programming languages and frameworks such as **Java/TestNG, Java/JUnit, Cucumber**, and others.  

All collected data is stored in **InfluxDB**, ensuring efficient time-series data management. Reports and visualizations are then generated using **Grafana**, enabling teams to monitor key performance indicators (KPIs) such as test coverage, defect trends, and automation efficiency. By providing real-time insights, the **QM KPI Metric Tool** supports data-driven decision-making and continuous quality improvement.  

---

Would you like to emphasize any specific KPIs or additional integrations?
