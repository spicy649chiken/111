# SZTU_get_grades

本仓库用于自动获取深圳技术大学教务系统的成绩，并通过邮件提醒你成绩变动。  
**注意成绩变动通过往年绩点变化判断，因此仅适用于大一第二学期及之后** 

---

## 步骤一：准备本地文件

确保文件夹中已经有以下两个文件，并已按要求内容更新：

- `get_grades.py` （即“智能推算版”主脚本）
- `requirements.txt` 内容如下：

  ```
  selenium>=4.0.0
  ```

---

## 步骤二：上传到 GitHub

在 GitHub 创建新仓库。
上传上述两个文件（`get_grades.py`、`requirements.txt`）到仓库。

---

## 步骤三：获取邮箱授权码（以 QQ 邮箱为例）

1. 登陆网页版 QQ 邮箱；
2. 点击左上角「设置」->「账户」；
3. 下拉，找到「POP3/IMAP/SMTP...服务」；
4. 保证「POP3/SMTP服务」已开启；
5. 点击下方“生成授权码”，获得一串英文字符（如 `abcdefghijklm`），记下它。

> ⚠️此授权码非邮箱密码，仅用于第三方发信。

---

## 步骤四：配置 GitHub Secrets （**关键**）

1. 打开你的 GitHub 仓库页面；
2. 点击顶部「Settings」；
3. 左侧找到「Secrets and variables」->「Actions」；
4. 点击右上角绿色 `New repository secret` 按钮；
5. 添加以下 5 个变量（区分大小写）：

| Name           | Value                | 说明                        |
|----------------|---------------------|-----------------------------|
| STU_ID         | 你的学号             | 教务系统账号                |
| STU_PWD        | 你的密码             | 教务系统密码                |
| MAIL_USER      | 你的QQ邮箱@qq.com    | 邮件发送账号                |
| MAIL_PASS      | 刚才获得的授权码     | QQ邮箱生成的授权码          |
| MAIL_RECEIVER  | 你的QQ邮箱@qq.com    | 接收提醒的邮箱，推荐同上     |

---

## 步骤五：创建定时任务（GitHub Actions Workflow）

1. 在项目页面顶部点击「Actions」；
2. 若页面为空，选择「set up a workflow yourself」或「New workflow」；
3. 默认文件名是 `main.yml`，可改为 `grade_monitor.yml`；
4. 在 `.github/workflows/grade_monitor.yml` 配置action：

---

## 步骤六：测试运行

1. 回到「Actions」页面；
2. 选择左侧 `GPA Monitor`;
3. 点击「Run workflow」->「Run workflow」；
4. 等待约 1 分钟：
    - 若运行成功（绿色 ✅），你的邮箱将收到“🔔 成绩单更新提醒！(首次运行...)”邮件；
    - 仓库将自动生成 `grade_history.json` 文件（可在代码页刷新查看）。

---

## 后续与说明

- **定时检测**：每1小时自动运行一次，无新成绩则无打扰。
- **新成绩出现时**：如有新课/排名变动，将立刻发邮件通知你。
- **绩点计算有误差**：由于均绩点四舍五入，因此计算的绩点仅供参考，不代表真实绩点
---

### 免责声明

- 请妥善保管好账号信息；
- 本项目仅供个人学习交流使用。

---

