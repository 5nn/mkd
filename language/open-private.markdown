        /访问控制语法
        //通过修饰符 open，public，internal，filepart，private 来声明实体的访问级别:

        //public class SomePublicClass {}
        //internal class SomeInternalClass {}//隐式内部访问级别
        //fileprivate class SomeFilePrivateClass {}
        //private class SomePrivateClass {}
        //
        //public var somePublicVariable = 0
        //internal let someInternalConstant = 0//隐式内部访问级别
        //fileprivate func someFilePrivateFunction() {}
        //private func somePrivateFunction() {}


        public class SomePublicClass { //显式公开类

            public var somePublicProperty = 0  //显式公开类成员
            var someInternalProperty = 0        //隐式内部成员

            fileprivate func someFilePrivateMethod() {} ///显式文件私有类成员
            private func somePrivateMethod() {}  //显式私有类成员
        }

        class SomeInternalClass {   //隐式内部类
            var someInternalProperty = 0    //隐式内部类成员
            fileprivate func someFilePrivateMethod() {} // 显式文件私有类成员
            private func somePrivateMethod() {} //显式私有类成员
        }

        fileprivate class SomeFilePrivateClass {// 显式文件私有类
            func someFilePrivateMethod() {} // 隐式文件私有类成员
            private func somePrivateMethod() {}// 显式私有类成员
        }

        private class SomePrivateClass { // 显式私有类
            func somePrivateMethod() {}// 隐式私有类成员
        }


        //open
        //
        //open 修饰的 class 在 Module 内部和外部都可以被访问和继承
        //open 修饰的 func 在 Module 内部和外部都可以被访问和重载（override）
        //Public
        //
        //public 修饰的 class 在 Module 内部可以访问和继承，在外部只能访问
        //public 修饰的 func 在 Module 内部可以被访问和重载（override）,在外部只能访问
        //Final
        //
        //final 修饰的 class 任何地方都不能不能被继承
        //final 修饰的 func 任何地方都不能被 Override
        //总结：
        //
        //现在的访问权限则依次为：open，public，internal，fileprivate，private