# TypeScript Snippets & Cheatsheet

TypeScriptでよく使う型定義やスニペットです。

---

## 基本的な型

```typescript
// プリミティブ型
let str: string = "hello";
let num: number = 123;
let bool: boolean = true;
let undef: undefined = undefined;
let nul: null = null;
let sym: symbol = Symbol('sym');
let big: bigint = 100n; // ES2020以降

// 配列
let arr1: number[] = [1, 2, 3];
let arr2: Array<string> = ['a', 'b'];

// タプル（要素の型と数が固定された配列）
let tuple: [string, number] = ["hello", 123];

// Any（どんな型でも許容、非推奨）
let dynamic: any = "can be anything";

// Unknown（安全なAny）
let unknownVar: unknown = "can be anything";
if (typeof unknownVar === 'string') {
  console.log(unknownVar.toUpperCase()); // 型ガードが必要
}

// Void（関数が何も返さない場合）
function logMessage(): void {
  console.log("Message");
}

// Never（到達不能なコードパス）
function error(message: string): never {
  throw new Error(message);
}

// インターフェース (interface)
interface User {
  id: number;
  name: string;
  email?: string; // オプショナルプロパティ
  readonly createdAt: Date; // 読み取り専用プロパティ
}

interface AdminUser extends User { // 継承
  role: 'admin';
  permissions: string[];
}

const normalUser: User = { id: 1, name: "Alice", createdAt: new Date() };
const adminUser: AdminUser = { id: 2, name: "Bob", role: 'admin', permissions: ['manageUsers'], createdAt: new Date() };

// 型エイリアス (type)
type ID = string | number; // Union型
type Point = {
  x: number;
  y: number;
};
type Status = 'active' | 'inactive' | 'pending'; // Literal Union型

type Employee = User & { salary: number }; // Intersection型 (インターフェースとも組み合わせ可)

const employee: Employee = { id: 3, name: "Charlie", createdAt: new Date(), salary: 50000 };

//Partial
interface UserProfile {
  name: string;
  age: number;
  city: string;
}

type PartialUserProfile = Partial<UserProfile>;
// { name?: string; age?: number; city?: string; }

const userUpdate: PartialUserProfile = { city: "Tokyo" };

// Readonly
interface Task {
  id: number;
  description: string;
}

type ReadonlyTask = Readonly<Task>;
// { readonly id: number; readonly description: string; }

const task: ReadonlyTask = { id: 1, description: "Complete report" };
// task.description = "New description"; // エラー: 読み取り専用プロパティのため

// Pick
interface Product {
  id: number;
  name: string;
  price: number;
  category: string;
}

type ProductSummary = Pick<Product, 'name' | 'price'>;
// { name: string; price: number; }

const summary: ProductSummary = { name: "Laptop", price: 1200 };

// Omit
interface Order {
  orderId: string;
  customerId: number;
  items: string[];
  totalAmount: number;
}

type OrderWithoutId = Omit<Order, 'orderId'>;
// { customerId: number; items: string[]; totalAmount: number; }

const newOrder: OrderWithoutId = { customerId: 101, items: ['Book'], totalAmount: 25 };

// Record
type Page = 'home' | 'about' | 'contact';
type PageInfo = { title: string; path: string };

type PageMap = Record<Page, PageInfo>;
/*
{
  home: { title: string; path: string; };
  about: { title: string; path: string; };
  contact: { title: string; path: string; };
}
*/

const pages: PageMap = {
  home: { title: "Home Page", path: "/" },
  about: { title: "About Us", path: "/about" },
  contact: { title: "Contact Us", path: "/contact" }
};

// 関数の型定義
type GreetFunction = (name: string) => string;

const greet: GreetFunction = (name) => `Hello, ${name}!`;

// オーバーロード
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
  return a + b;
}

// クラスの型定義
class Greeter {
  greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }

  greet(): string {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");

// Reactイベントハンドラの型（Frontend向け）
import React from 'react';

// ボタンクリックイベント
const handleClick = (event: React.MouseEvent<HTMLButtonElement>) => {
  console.log(event.currentTarget.tagName); // "BUTTON"
};

// インプット変更イベント
const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
  console.log(event.target.value); // 入力された値
};

// フォーム送信イベント
const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
  event.preventDefault(); // デフォルトのフォーム送信を防止
  console.log("Form submitted!");
};