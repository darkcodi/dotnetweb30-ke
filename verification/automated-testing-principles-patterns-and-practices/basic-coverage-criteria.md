# Basic coverage criteria

There are a number of coverage criteria, the main ones being:

* **Function coverage** – Has each function \(or subroutine\) in the program been called?
* **Statement coverage/Code coverage** – Has each statement/LOC in the program been executed?
* **Edge coverage –** Has every edge in the Control flow graph been executed?
* **Branch coverage** – Has each branch \(also called DD-path\) of each control structure \(such as in if and case statements\) been executed? For example, given an if statement, have both the true and false branches been executed? Notice that this one is a subset of **Edge coverage.**
* **Condition coverage** \(or predicate coverage\) – Has each Boolean sub-expression evaluated both to true and false?

### Code coverage vs branch coverage example

#### Code coverage

![](../../.gitbook/assets/image%20%2826%29.png)

![](../../.gitbook/assets/image%20%2857%29.png)

4/5 = **80%**

#### **Branch coverage**

![](../../.gitbook/assets/image%20%28109%29.png)

![](../../.gitbook/assets/image%20%28167%29.png)

3/3 = **100%**

