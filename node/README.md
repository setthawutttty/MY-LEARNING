# Install
```
npm init
```

# Express
```
npm i express //ติดตั้ง express

```

# Nodemon hot-reload
```
npm i nodemon --save-dev // บันทึกเก็บไว้ เฉพาะ dev ไม่เอาขึ้น server

เมื่อต้องการรัน แบบ npm run dev| ไปแก้ที่ script
  "scripts": {
    "dev": "nodemon index.js"
  },

```

# ตัวอย่างไฟล์ router
```
โฟร์เดอร์(ชื่อ)/
      │
      ├─── controller/
      │      └─ userController.js
      │
      ├─── router/
      │      ├─ index.js
      │      └─ userRouter.js
      │
      └─── index.js


─────────────────────────────────────────────────────────────────────────────────────
userController.js
----------------------------
const userController = {
  helloHome: (req, res) => {
    res.send('hello home')
  },
  hellotest: (req, res) => {
    res.send('hello test')
  },
  hellotee: (req, res) => {
    res.send('hello tee')
  },
};

export default userController;
#######################################################
─────────────────────────────────────────────────────────────────────────────────────
router index.js
----------------------------
import express from "express";
import userRouter from "./userRouter.js";

const router = express.Router();
userRouter(router);

export default router;
#######################################################
─────────────────────────────────────────────────────────────────────────────────────
userRouter.js
----------------------------
import userController from "../controllers/userController.js";

const userRouter = (items) => {
  items.get("/", userController.helloHome);
  items.get("/test", userController.hellotest);
  items.get("/tee", userController.hellotee);
};

export default userRouter;
#######################################################
─────────────────────────────────────────────────────────────────────────────────────
index.js
----------------------------
import express from "express";
import router from "./router/index.js";

const app = express();
const port = 3000;

app.use(router);

app.listen(port);

#######################################################
─────────────────────────────────────────────────────────────────────────────────────
```
