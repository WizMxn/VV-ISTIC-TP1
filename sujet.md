# Practical Session #1: Introduction

## 1 - Find in news sources a general public article reporting the discovery of a software bug.

[Faulty Firmware Auto-Update Breaks Hundreds of 'Smart Locks'](https://thehackernews.com/2017/08/firmware-smart-locks.html)

### Describe the Bug
Hundreds of Internet-connected locks became inoperable after a faulty software update was mistakenly sent to certain models. This issue rendered the built-in keypad on the affected smart lock devices unusable, preventing users from unlocking their doors.

### Nature of the Bug
The bug is global in scope, as it affects all devices of a specific model that received the erroneous update. The failure occurred because the firmware update, intended for the 7000i model smart locks, was mistakenly deployed to 6000i model products instead.

### Repercussions for Clients and the Company
The consequences of this bug are severe for both users and the manufacturer:

1. **For Consumers**:
    - The affected smart locks cannot reconnect to the company's web servers, making a remote fix impossible.
    - Consumers are left with two inconvenient options:  
      a) Remove the back flap of the lock and send it to the manufacturer for manual firmware updating, which takes 5-7 working days.  
      b) Request a replacement lock, which takes 14-18 days to ship, after which they must return the faulty model.

2. **For the Company**:
    - The company faces reputational damage due to the inconvenience caused to consumers.
    - There are likely additional costs associated with handling returns, replacements, and manual updates.

### Could Proper Testing Have Prevented This?
Yes, proper testing could have identified this issue. Specifically:
- Tests should have been conducted to ensure the update was only sent to the correct device models.
- A scenario where the update is mistakenly sent to other versions should have been simulated to verify that the locks remain operational or the update is rejected outright.

---
## Apache Commons projects
[Link for the issues](https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues)
###  Among those issues find one that corresponds to a bug that has been solved. 
[[COLLECTIONS-796] - SetUniqueList.createSetBasedOnList doesn't add list elements to return value](https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-796?filter=doneissues)
### Classify the bug as local or global. 

Local, a developer "accidentally" remove a line from a method, and nobody review or ask why he did that. Nobody know today why this line was remove.

### Explain the bug and the solution.
The method createSetBasedOnList of the SetUniqueList class was set to return the intended Set based of the List type provided and populated it with all the elements of the List. But for some reason this [PR](https://github.com/apache/commons-collections/commit/b1c45ac691d46a8c609f2534d2adfa59c0599527#diff-8e53271d5d8299a76d43b0e3c81740fbe660083ae71c5bf2be63846d52156f23L344), with the title `Replace use of deprecated Class#newInstance()` remove the line `subSet.addAll(list);
` at the end of the method. The fix was to roll back this delete.
### Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

Yes, it executes the method and check that for each element it is in the created set and the type is correct.

---

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

---

## WebAssembly

### Advantages of Having a Formal Specification for WebAssembly

WebAssembly’s **formal specification** offers significant benefits:

#### 1. **Consistency Across Platforms**
- Ensures WebAssembly behaves identically across all platforms, crucial for its use in various environments.

#### 2. **Predictability and Reliability**
- Guarantees programs will execute as expected, reducing surprises from differing implementations.

#### 3. **Soundness of Execution**
- Ensures **type safety** and **memory safety**, preventing errors like invalid memory access or unsafe type conversions.

#### 4. **Simplified Tooling**
- Enables the creation of reliable tools like validators and compilers directly aligned with formal rules.

#### 5. **Security**
- Prevents malicious programs from escaping their designated environment, minimizing vulnerabilities.

---

### Does This Mean WebAssembly Should Not Be Tested?

No, testing is still essential:

#### 1. **Implementation Errors**
- Developers implementing WebAssembly engines may make mistakes; testing ensures adherence to the specification.

#### 2. **Edge Cases and Real-World Scenarios**
- Testing verifies that WebAssembly handles unexpected scenarios and practical applications effectively.

#### 3. **Performance and Interoperability**
- Testing ensures optimizations and interactions with host systems (e.g., JavaScript APIs) are seamless and reliable.

#### 4. **Hardware Variability**
- Confirms WebAssembly runs smoothly on diverse devices and architectures.

---

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?


The mechanized specification of WebAssembly using Isabelle offers key advantages: enhanced reliability, proof automation, and executable semantics. It improved the original formal specification by identifying ambiguities and errors and enabled artifacts like executable models and safety proofs. The author verified the specification through formal proofs in Isabelle, ensuring correctness. However, it doesn’t eliminate the need for testing, as implementation bugs and environmental factors still require empirical validation.
## Answers
