Hi Christine,

I've gathered some data based on what you sent us. Please review the information we've found and let us know if it's correct.

For any projects where I couldn't find a corresponding qTest/JIRA entry, I've marked them with a question mark.

Once you confirm the current project list and, if possible, provide details for the questioned projects, we will proceed with granting access to you and your team.

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
