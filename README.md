### 单元测试
>- 测试包含单元测试，性能测试，安全测试和功能测试等几个方面。单元测试主要包含断言，测试框架，测试用例，测试覆盖率，mock, 持续集成等几个方面。

>单元测试是什么？
>- 对于前端开发来说，为了检测特定的代码是否达到预期的运行结果而采用专门的工具或方法来验证，并最终得到特定的结果。这样方便问题的排查和后期的修正。

>为什么需要单元测试？
>- 首先一个前端单元测试的原因是，JS是动态语言，缺少类型检查，编译期间无法定位到错误。
>- 单元测试可以检测代码的正确性，在上线前做到心里有底。
>- 单元测试可以自动化，通过编写测试用例，可以做到一次编写，多次运行。
>- 驱动开发，代码被测试的前提是代码本身是可测试的，要保证代码的可测试性，就需要在开发中注意API的设计， 注意代码职责的单一性。

>如何写单元测试用例？
>- 测试代码时，只考虑测试，不考虑内部实现
>- 数据尽量模拟实现，越靠近实现越好
>- 充分考虑数据的边界条件
>- 对重点、复杂、核心代码重点测试
