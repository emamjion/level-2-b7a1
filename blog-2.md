# কীভাবে Pick এবং Omit Utility Types Code Duplication কমায়?

## Introduction

TypeScript এ অনেক সময় একটি বড় interface থেকে ছোট ছোট specialized version তৈরি করার প্রয়োজন হয়। যদি প্রতিবার নতুন interface manually লিখতে হয়, তাহলে একই code বারবার লিখতে হয়। এটি code duplication তৈরি করে।

এই সমস্যা সমাধানের জন্য TypeScript এ Pick এবং Omit utility types ব্যবহার করা হয়। এগুলো master interface থেকে প্রয়োজনীয় অংশ নিয়ে নতুন type তৈরি করতে সাহায্য করে এবং code কে DRY (Don't Repeat Yourself) রাখে।

---

## Pick কী?

Pick ব্যবহার করা হয় একটি interface থেকে নির্দিষ্ট কিছু property নেওয়ার জন্য।

Example:

```ts
interface User {
  id: number;
  name: string;
  age: number;
  phone: number;
}

type UserProfile = Pick<User, "name" | "age">;
```

এখানে UserProfile type শুধুমাত্র name এবং age property পেয়েছে।

Result:

```ts
{
  name: string;
  age: string;
}
```

---

## Omit কী?

Omit ব্যবহার করা হয় একটি interface থেকে নির্দিষ্ট কিছু property বাদ দেওয়ার জন্য।

Example:

```ts
interface User {
  id: number;
  name: string;
  age: number;
  phone: number;
}

type PublicUser = Omit<User, "phone">;
```

এখানে phone property বাদ গেছে।

Result:

```ts
{
  id: number;
  name: string;
  age: number;
}
```

---

## কীভাবে এগুলো Code Duplication কমায়?

ধরি আমার একটি বড় User interface আছে। এখন profile page, admin panel — সব জায়গায় different version দরকার।

যদি manually লিখি:

```ts
interface UserProfile {
  name: string;
  email: string;
}

interface PublicUser {
  id: number;
  name: string;
  email: string;
}
```

তাহলে একই property বারবার লিখতে হচ্ছে।

কিন্তু Pick এবং Omit ব্যবহার করলে main interface থেকেই দরকারি অংশ নিয়ে নতুন type তৈরি করা যায়।

এতে:

- একই code বারবার লিখতে হয় না
- maintenance সহজ হয়
- ভুল হওয়ার সম্ভাবনা কমে
- code clean থাকে

---

## DRY (Don't Repeat Yourself) Principle

DRY মানে হলো একই logic বা structure বারবার না লেখা।

Pick এবং Omit DRY principle follow করতে সাহায্য করে কারণ:

- একটি main interface maintain করলেই হয়
- সব related type automatically update করা যায়
- duplicate code কমে যায়

ধরি User interface এ নতুন property যোগ করতে হলো:

```ts
age: number;
```

এখন Pick বা Omit ব্যবহার করা সব type automatically update হয়ে যাবে। আলাদা আলাদা interface modify করতে হবে না।

---

## Conclusion

Pick এবং Omit utility types TypeScript এ খুব গুরুত্বপূর্ণ কারণ এগুলো master interface থেকে প্রয়োজনীয় অংশ নিয়ে specialized type তৈরি করতে সাহায্য করে।

এর ফলে code duplication কমে, maintenance সহজ হয় এবং DRY principle বজায় থাকে। তাই বড় project এ clean এবং reusable code লেখার জন্য Pick এবং Omit অনেক useful।
