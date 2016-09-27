#class

1. 자바스크립트에서도 class 생성이 가능
2. private, public, protected 와 같은 접근자 선언은 안됨
3. 상속은 가능(단일 상속만 가능)
4. 생성자는 constructer를 이용
5. static 으로 전역 함수 선언 가능

```javascript
class Shape {
    constructor (id, x, y) {
        this.id = id;
        this.x = x;
        this.y = y;
    }
    
    static test1() {
      console.log('static 함수 테스트');
    }
    
    size() {
        return this.x * this.y;
    }
    
    toString () {
        return `Shape(${this.id}, ${this.size()})`
    }
}
class Rectangle extends Shape {
    constructor (id, x, y, width, height) {
        super(id, x, y);
        this.width = width;
        this.height = height;
    }
    
    size() {
        return super.size() * this.width * this.height;
    }
    
    toString () {
        return `Rectangle(${this.size()}) > ` + super.toString();
    }
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        super(id, x, y);
        this.radius = radius;
    }
    
    size() {
        return super.size() * this.radius;            
    }
    
    toString () {
        return `Circle(${this.size()}) > ` + super.toString()
    }
}

const shape = new Shape('shape', 1,2);
Shape.test1(); 
console.log(shape.toString());

const rectangle = new Rectangle('shape', 1,2, 10, 20);
console.log(rectangle.toString());
const circle = new Circle('shape', 1,2, 10);
console.log(circle.toString());
```
