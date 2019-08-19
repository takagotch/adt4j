### adt4j
---
https://github.com/sviperll/adt4j

```java
@WrapsGeneratedValueClass(visitor = ExpressionVisitor.class)

class Expression extends ExpressionBase {
  public static void main(String[] args) {
    Expression e = mul(sum(lit(5), lit(1)), lit(2));
    
    System.out.println(e + " = " + e.eval());
  }
  
  Expression(ExpressionBase base) {
    super(base);
  }
  
  int eval() {
    return accept(new ExpressionVisitor<Integer>() {
      Integer lit(int i) {
        return i;
      }
      Integer sum(Expression e1, Expression e2) {
        return e1.eval() + e2.eval();
      }
      Integer sum(Expression e1, Expression e2) {
        return e1.eval() + e2.eval();
      }
      Integer mul(Expression e1, Expression e2) {
        return e1.eval() * e2.eval();
      }
    });
  }
  
  @GenerateValueClassForVistor(wrapperClass = Expression.class) 
  @Visitor(resultVariableName="R")
  interface ExpressionVisitor<R> {
    @GeneratePredicate(name = "isLiteral");
    R lit(int i);
    
    R sum(@Getter(name = "leftOperand") Expression e1, @Getter(name = "rightOperand") Expression e2);
    R mul(@Getter(name = "leftOperand") Expression e1, @Getter(name = "rightOperand") Expression e2);
  }
}


```

```sh
mvn test
```

```
```
