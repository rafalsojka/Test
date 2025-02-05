import com.atlassian.jira.component.ComponentAccessor
import com.atlassian.jira.issue.link.IssueLinkManager
import com.atlassian.jira.issue.watchers.WatcherManager

def issue = event.issue
def issueLinkManager = ComponentAccessor.getIssueLinkManager()
def watcherManager = ComponentAccessor.getWatcherManager()

// Check for "Cloners" link type (incoming link)
def clonedFromIssue = issueLinkManager.getInwardLinks(issue.id)
    .find { it.issueLinkType.name == "Cloners" }?.sourceObject

if (clonedFromIssue) {
    log.debug("Issue ${issue.key} was cloned from ${clonedFromIssue.key}")

    // Copy watchers
    def watchers = watcherManager.getWatchers(clonedFromIssue)
    watchers.each { watcherManager.startWatching(it, issue) }

    log.debug("Copied ${watchers.size()} watchers to ${issue.key}")
}
