import javax.naming.*;
import javax.naming.directory.*;
import java.util.Hashtable;

public class ActiveDirectoryQuery {
    public static void main(String[] args) {
        // Active Directory connection details
        String ldapURL = "ldap://your-ad-server:389"; // Replace with your AD server and port
        String searchBase = "dc=example,dc=com"; // Replace with your domain
        String searchFilter = "(sAMAccountName=jdoe)"; // Replace with your search filter
        String bindDN = "your-username@example.com"; // Replace with your username
        String bindPassword = "your-password"; // Replace with your password

        // Set up the environment for creating the initial context
        Hashtable<String, String> env = new Hashtable<>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
        env.put(Context.PROVIDER_URL, ldapURL);
        env.put(Context.SECURITY_AUTHENTICATION, "simple");
        env.put(Context.SECURITY_PRINCIPAL, bindDN);
        env.put(Context.SECURITY_CREDENTIALS, bindPassword);

        try {
            // Create the initial context
            DirContext ctx = new InitialDirContext(env);
            System.out.println("Connection established!");

            // Set up the search controls
            SearchControls searchControls = new SearchControls();
            searchControls.setSearchScope(SearchControls.SUBTREE_SCOPE);

            // Perform the search
            NamingEnumeration<SearchResult> results = ctx.search(searchBase, searchFilter, searchControls);

            // Process the search results
            while (results.hasMore()) {
                SearchResult result = results.next();
                System.out.println("Found entry: " + result.getNameInNamespace());

                Attributes attrs = result.getAttributes();
                NamingEnumeration<? extends Attribute> attributes = attrs.getAll();
                while (attributes.hasMore()) {
                    Attribute attr = attributes.next();
                    System.out.println(attr.getID() + ": " + attr.get());
                }
            }

            // Close the context
            ctx.close();
            System.out.println("Connection closed!");
        } catch (NamingException e) {
            e.printStackTrace();
        }
    }
}
