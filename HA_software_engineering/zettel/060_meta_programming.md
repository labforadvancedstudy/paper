# 060_meta_programming

## 코드를 쓰는 코드 (Code That Writes Code)

**Level**: L7 - 재귀적 추상화 (Recursive Abstraction)
**Date**: 2025-06-21
**Reference**: [057_software_as_thought](057_software_as_thought.md), [030_recursion](030_recursion.md)
**Tags**: #metaprogramming #recursion #abstraction #code-generation #reflection

## 개념 (Concept)

메타프로그래밍은 프로그램을 데이터로 다루는 기술이다. 코드가 코드를 읽고, 분석하고, 변형하고, 생성한다. 그것은 프로그래밍의 프로그래밍이며, 추상화의 궁극적 형태다.

## 원리 (Principle)

```
Meta Levels:
Level 0: 데이터를 다루는 코드
Level 1: 코드를 다루는 코드 (메타프로그래밍)
Level 2: 메타프로그램을 다루는 코드
Level ∞: 무한 재귀의 가능성

Techniques:
- Reflection: 자기 검사
- Code Generation: 코드 생성
- Macros: 구문 변환
- Templates: 타입 레벨 계산
- Eval: 동적 실행
```

## 통찰 (Insights)

### 1. 코드-데이터 동치성
```python
# Lisp의 통찰: 코드 = 데이터
code_as_data = ['def', 'add', ['a', 'b'], 
                ['return', ['+', 'a', 'b']]]

# Python의 AST
import ast
code = "x + y"
tree = ast.parse(code)
# 코드를 트리 구조로 조작
modified = transform(tree)
new_code = compile(modified, '<string>', 'eval')
```

### 2. 자기 참조의 힘
```python
class MetaClass(type):
    """클래스를 만드는 클래스"""
    def __new__(meta, name, bases, attrs):
        # 클래스 생성 시점에 개입
        attrs['created_at'] = time.time()
        attrs['meta_info'] = f"Created by {meta}"
        return super().__new__(meta, name, bases, attrs)

class SelfAware(metaclass=MetaClass):
    """자신이 어떻게 만들어졌는지 아는 클래스"""
    pass
```

### 3. 코드 생성기
```python
def generate_class(name, fields):
    """동적으로 클래스 생성"""
    code = f"class {name}:\n"
    code += "    def __init__(self, " + ", ".join(fields) + "):\n"
    for field in fields:
        code += f"        self.{field} = {field}\n"
    
    exec(code, globals())
    return globals()[name]

# 런타임에 클래스 생성
Person = generate_class("Person", ["name", "age"])
p = Person("Alice", 30)
```

## 실재 (Reality)

메타프로그래밍의 실제 활용:

```python
# ORM: 데이터베이스 스키마에서 클래스 생성
class User(Model):
    name = StringField()
    age = IntegerField()
    # 메타클래스가 SQL 쿼리 메서드를 자동 생성

# 데코레이터: 함수를 변형하는 함수
@memoize
def expensive_computation(n):
    # 데코레이터가 캐싱 로직을 주입
    return complex_calculation(n)

# 템플릿 엔진: 코드로 HTML 생성
template = Template("Hello {{ name }}!")
html = template.render(name="World")

# 컴파일러: 언어를 다른 언어로
def compile_to_js(python_code):
    ast = parse(python_code)
    js_code = transform_to_javascript(ast)
    return js_code
```

## 철학적 함의 (Philosophical Implications)

1. **자기 지시의 역설**: 자신을 완전히 기술하는 프로그램은 가능한가?
2. **추상화의 한계**: 메타의 메타의 메타... 어디까지?
3. **창조자와 피조물**: 코드가 더 나은 코드를 만들 수 있는가?
4. **의미의 계층**: 각 메타 레벨에서 의미는 어떻게 변하는가?

## 실용적 지혜 (Practical Wisdom)

```python
def metaprogramming_wisdom():
    """메타프로그래밍의 지혜로운 사용"""
    
    # 1. 명확성 우선
    def clear_over_clever():
        # 메타프로그래밍은 강력하지만 복잡
        if simple_solution_exists():
            return use_simple_solution()
        else:
            return use_metaprogramming()
    
    # 2. 디버깅 고려
    def debuggable_meta():
        # 생성된 코드도 디버깅 가능해야
        generated = generate_code()
        generated_with_debug = add_source_mapping(generated)
        return generated_with_debug
    
    # 3. 타입 안전성
    def type_safe_meta():
        # 가능하면 정적 타입 검사 유지
        return use_generics_over_string_eval()
```

## 연결 (Connections)

- [030_recursion](030_recursion.md) - 자기 참조의 기초
- [057_software_as_thought](057_software_as_thought.md) - 메타 사고
- [014_abstraction](014_abstraction.md) - 추상화의 극한
- [063_artificial_intelligence](063_artificial_intelligence.md) - 스스로 프로그래밍하는 AI

## 성찰 (Reflection)

메타프로그래밍은 프로그래밍의 거울이다. 코드가 자신을 바라보고, 이해하고, 변형한다. 이것은:

1. **힘의 증폭**: 적은 코드로 많은 코드 생성
2. **유연성의 극대화**: 런타임에 구조 변경
3. **추상화의 정점**: 패턴의 패턴을 다루기
4. **위험의 증가**: 큰 힘에는 큰 책임이

"코드를 쓰는 코드를 쓰는 프로그래머" - 우리는 몇 차원을 다루고 있는가?

## 더 깊이 (Deeper Dive)

```python
class DeeperMeta:
    """메타프로그래밍의 심연"""
    
    def quine(self):
        """자기 자신을 출력하는 프로그램"""
        s = 's = %r; print(s %% s)'; print(s % s)
    
    def homoiconicity(self):
        """코드와 데이터의 완전한 동일성"""
        # Lisp이 보여준 길
        return code_is_data_is_code
    
    def metacircular_evaluator(self):
        """자기 자신으로 자신을 구현"""
        def eval_in_itself(expr, env):
            if is_symbol(expr):
                return env[expr]
            elif is_list(expr):
                func = eval_in_itself(expr[0], env)
                args = [eval_in_itself(arg, env) 
                       for arg in expr[1:]]
                return func(*args)
    
    def infinite_tower(self):
        """메타의 무한 탑"""
        # 각 레벨이 아래 레벨을 해석
        return interpreters_all_the_way_up()
```

메타프로그래밍은 코드의 자기 인식이다. 그것은 소프트웨어가 자신의 본질을 이해하려는 시도다.