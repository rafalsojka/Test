Below is an example of a Python test containing 20 questions. These questions are designed to be conceptually similar to those found in Java OCP (Oracle Certified Professional) exams but adapted to Python.


---

Python OCP-Style Test

1. What will the following code output?

x = [1, 2, 3]
y = x
y.append(4)
print(x)

A) [1, 2, 3]

B) [1, 2, 3, 4]

C) [1, 2]

D) Error


Answer: B


---

2. What is the output of the following code?

def func(a, b=[]):
    b.append(a)
    return b

print(func(1))
print(func(2))

A) [1] [2]

B) [1] [1, 2]

C) [1] []

D) Error


Answer: B


---

3. Which of the following is true about Python sets?

A) Sets allow duplicate values.

B) Sets are mutable.

C) Sets maintain insertion order.

D) Sets are indexed.


Answer: B


---

4. What is the output of the following code?

x = "Python"
print(x[1:4])

A) Pyt

B) yth

C) ytho

D) Error


Answer: B


---

5. Which of the following methods is used to remove an element from a dictionary by its key?

A) delete

B) pop

C) remove

D) discard


Answer: B


---

6. What will the following code output?

x = (1, 2, 3)
x[0] = 10
print(x)

A) (10, 2, 3)

B) (1, 10, 3)

C) Error

D) None of the above


Answer: C


---

7. What is the output of the following code?

a = [1, 2, 3]
b = [4, 5, 6]
c = zip(a, b)
print(list(c))

A) [(1, 2), (3, 4)]

B) [(1, 4), (2, 5), (3, 6)]

C) [(4, 5, 6)]

D) Error


Answer: B


---

8. Which of the following creates a generator in Python?

A) []

B) {}

C) ()

D) yield


Answer: D


---

9. What will the following code output?

print(bool(0), bool(""), bool([]))

A) False False True

B) True True False

C) False False False

D) True False False


Answer: C


---

10. What is the result of the following code?

a = {1, 2, 3}
b = {3, 4, 5}
print(a & b)

A) {1, 2, 3, 4, 5}

B) {3}

C) {1, 2}

D) Error


Answer: B


---

11. What is the output of the following code?

x = "Hello"
print(x[::-1])

A) olleH

B) Hello

C) Error

D) None of the above


Answer: A


---

12. How do you handle exceptions in Python?

A) try...except

B) try...catch

C) try...handle

D) None of the above


Answer: A


---

13. What will this code output?

class Example:
    def __init__(self, x):
        self.x = x

e1 = Example(5)
e2 = e1
e2.x = 10
print(e1.x)

A) 5

B) 10

C) Error

D) None of the above


Answer: B


---

14. What is the purpose of the is keyword in Python?

A) Compare object values.

B) Compare object identities.

C) Assign values.

D) None of the above.


Answer: B


---

15. What is the difference between a list and a tuple in Python?

A) Lists are mutable, tuples are immutable.

B) Lists are immutable, tuples are mutable.

C) Both are mutable.

D) Both are immutable.


Answer: A


---

16. What does the following code do?

a = [1, 2, 3]
b = [4, 5, 6]
c = a + b

A) Combines two lists into one.

B) Multiplies two lists.

C) Raises an error.

D) None of the above.


Answer: A


---

17. Which of the following is not a valid Python data type?

A) List

B) Dictionary

C) Stack

D) Set


Answer: C


---

18. What will the following code output?

def greet(name="User"):
    return f"Hello, {name}!"

print(greet("Alice"))
print(greet())

A) Hello, Alice! Hello, User!

B) Hello, User! Hello, Alice!

C) Hello, Alice! Error

D) None of the above


Answer: A


---

19. Which statement about Python modules is true?

A) Modules cannot be imported.

B) Python files with .py extensions can be modules.

C) Modules must start with an underscore.

D) None of the above.


Answer: B


---

20. What is the purpose of the super() function in Python?

A) To call the parent class's methods.

B) To define a subclass.

C) To raise an exception.

D) None of the above.


Answer: A


---

This test provides a mix of syntax, conceptual, and practical questions about Python programming, mirroring the complexity and structure of Java OCP questions.

import javax.net.ssl.*;
import java.security.cert.X509Certificate;

public class DisableCertValidation {
    public static void disable() throws Exception {
        TrustManager[] trustAllCerts = new TrustManager[]{
            new X509TrustManager() {
                public X509Certificate[] getAcceptedIssuers() {
                    return null;
                }
                public void checkClientTrusted(X509Certificate[] certs, String authType) {}
                public void checkServerTrusted(X509Certificate[] certs, String authType) {}
            }
        };

        // Install the all-trusting trust manager
        SSLContext sc = SSLContext.getInstance("TLS");
        sc.init(null, trustAllCerts, new java.security.SecureRandom());
        HttpsURLConnection.setDefaultSSLSocketFactory(sc.getSocketFactory());

        // Optionally disable hostname verification
        HostnameVerifier allHostsValid = (hostname, session) -> true;
        HttpsURLConnection.setDefaultHostnameVerifier(allHostsValid);
    }
}
