---
description: Observables are lazy Push collections of multiple values.
---

# Observable



|  | SINGLE | MULTIPLE |
| :--- | :--- | :--- |
| Pull | Function | Iterator |
| Push | Promise | Observable |

### **Pull versus Push**

_Pull_ and _Push_ are two different protocols that describe how a data _Producer_ can communicate with a data _Consumer_.

**What is Pull?** In Pull systems, the Consumer determines when it receives data from the data Producer. The Producer itself is unaware of when the data will be delivered to the Consumer.

**What is Push?** In Push systems, the Producer determines when to send data to the Consumer. The Consumer is unaware of when it will receive that data.

Pull versus Push

|  | PRODUCER | CONSUMER |
| :--- | :--- | :--- |
| Pull | Passive: produces data when requested. | Active: decides when data is requested. |
| Push | Active: produces data at its own pace. | Passive: reacts to received data. |

> Subscribing to an Observable is analogous to calling a Function.

## 🎯 Anatomy of an Observable

Observables are created using new Observable or a creation operator, are subscribed to with an Observer, execute to deliver next / error / complete notifications to the Observer, and their execution may be disposed.

**Core Observable concerns:**

* **Creating** Observables
* **Subscribing** to Observables
* **Executing** the Observable
* **Disposing** Observables

