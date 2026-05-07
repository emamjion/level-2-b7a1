# কেন any কে TypeScript এ "Type Safety Hole" বলা হয়?

## Introduction

TypeScript মূলত JavaScript কোডকে আরও safe করার জন্য তৈরি করা হয়েছে। এটি code run হওয়ার আগেই type checking করে error ধরতে সাহায্য করে। কিন্তু any type ব্যবহার করলে TypeScript এর এই safety system কাজ করা বন্ধ করে দেয়। এজন্য any কে অনেক সময় "type safety hole" বলা হয়।

অন্যদিকে unknown হলো safer option, কারণ এটি type check ছাড়া value ব্যবহার করতে দেয় না।

---

## কেন any কে "Type Safety Hole" বলা হয়?

যখন কোনো variable এর type any দেওয়া হয়, তখন TypeScript আর সেই variable এর type check করে না। ফলে যেকোনো ধরনের operation করা যায়, এমনকি ভুল operation হলেও compile time এ error দেখায় না।

Example:

```ts
let value: any = "Programmming Hero";

value = 101;

value.toUpperCase();
```

এখানে প্রথমে value একটি string ছিল, পরে সেটি number হয়ে গেছে। তারপরও toUpperCase() ব্যবহার করা হয়েছে।

TypeScript error দেখায়নি কারণ variable এর type ছিল any।

কিন্তু code run করলে runtime error হবে।

---

## কেন unknown বেশি Safe?

unknown type safer কারণ এটি value এর type check না করে সরাসরি ব্যবহার করতে দেয় না।

Example:

```ts
let value: unknown = "Programming Hero";

if (typeof value === "string") {
  value.toUpperCase();
}
```

এখানে typeof দিয়ে check করার পরে TypeScript বুঝতে পারে যে value একটি string। এরপরই toUpperCase() ব্যবহার করা সম্ভব হয়।

এভাবে unknown runtime error হওয়ার সম্ভাবনা কমিয়ে দেয়।

---

## Type Narrowing কী?

Type narrowing হলো এমন একটি process যেখানে TypeScript condition ব্যবহার করে variable এর নির্দিষ্ট type শনাক্ত করে।

সাধারণত নিচের জিনিসগুলো ব্যবহার করে type narrowing করা হয়:

- typeof
- instanceof
- in

Example:

```ts
let data: unknown = 10;

if (typeof data === "number") {
  return data.toFixed(2);
}
```

এখানে typeof check করার পরে TypeScript বুঝতে পারে যে data একটি number।

এই process কেই type narrowing বলা হয়।

---

## Conclusion

any কে "type safety hole" বলা হয় কারণ এটি TypeScript এর type checking বন্ধ করে দেয় এবং runtime error এর সম্ভাবনা বাড়ায়।

অন্যদিকে unknown safer কারণ এটি value ব্যবহার করার আগে type check করতে বাধ্য করে। Type narrowing ব্যবহার করে unknown data নিরাপদভাবে handle করা যায় এবং TypeScript এর type safety বজায় থাকে।