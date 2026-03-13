# ABAP-RESTful-Application
sap-hr-leave-request-app か abap-rap-hr-leave-request 

# SAP HR Leave Request Mini

SAP HRで扱う休暇申請業務を題材に、社員による休暇申請、承認者による承認／差戻し、残日数チェックを小規模に再現するポートフォリオです。

本プロジェクトは、ABAP RESTful Application Programming Model (RAP) と SAP Fiori elements を用いて、業務システムらしい入力・一覧・承認フローを再現することを目的としています。

## 背景

過去にSAP HR周辺業務に触れた経験を振り返りながら、休暇申請という比較的小さな業務を題材にして、自分なりに再整理・再現するために作成しています。

大規模な人事システム全体ではなく、以下のような最小限の業務フローに絞っています。

- 社員が休暇を申請する
- 承認者が内容を確認する
- 承認または差戻しする
- 承認済みの場合のみ残日数を反映する

## 目的

- SAP HR系業務の流れを整理し直す
- RAPで業務オブジェクトを作る
- Fiori elementsで一覧・詳細・登録画面を構築する
- 業務ルールを意識した最小アプリをポートフォリオ化する

## 想定機能

- 社員一覧参照
- 休暇申請登録
- 申請一覧表示
- 申請詳細表示
- 承認／差戻し
- 残日数チェック
- 重複申請チェック
- ステータス管理

## 想定業務ルール

- 残日数が不足している場合は申請不可
- 開始日が終了日より後の場合は申請不可
- 同一社員・同一日付で重複する申請は不可
- 差戻し時は理由必須
- 承認済みになった時点で残日数を減算
- 取消済み・差戻し済みの申請は残数減算対象外

## 技術構成

- SAP BTP ABAP Environment / ABAP Platform 想定
- ABAP RAP
- CDS View Entity
- Behavior Definition / Behavior Implementation
- OData Service Binding
- SAP Fiori elements

RAPでは、サービスバインディングを通じてOData公開とFiori Elementsプレビューが可能です。  
また、CDSのUIアノテーションによりFiori Elementsの画面表現を制御できます。  [oai_citation:1‡SAP](https://developers.sap.com/tutorials/abap-environment-restful-programming-model..html?utm_source=chatgpt.com)

## 画面想定

1. Employee List
2. Leave Request List Report
3. Leave Request Object Page
4. Create Leave Request
5. Approve / Reject Action

## データモデル概要

### Employee
- 社員ID
- 氏名
- 部署
- 承認者ID
- 有給残日数

### Leave Request
- 申請ID
- 社員ID
- 休暇種別
- 開始日
- 終了日
- 申請日数
- 理由
- ステータス
- 差戻し理由
- 承認者ID
- 登録日時
- 更新日時

### Leave Type
- 休暇種別コード
- 名称
- 控除対象フラグ

## 今後の拡張案

- 半休対応
- 祝日／休日考慮
- ワークフロー強化
- 権限制御
- Draft対応
- Launchpad配置

ABAP環境ではFiori LaunchpadやFioriアプリへのアクセス基盤が提供されています。  [oai_citation:2‡SAPヘルプポータル](https://help.sap.com/docs/sap-btp-abap-environment/abap-environment/ui-development-overview?locale=ja-JP&utm_source=chatgpt.com)

## このリポジトリで見せたいこと

- SAP寄りの業務理解
- 最小単位での要件整理
- RAPを使った業務アプリ設計
- Fioriでの一覧／詳細／登録体験
- ポートフォリオとしての構成力


# SAP HR Leave Request Mini

This portfolio project recreates a small leave request process inspired by SAP HR-related business operations.

The goal is to build a compact business application with employee leave request creation, approval/rejection flow, and leave balance validation using ABAP RESTful Application Programming Model (RAP) and SAP Fiori elements.

## Background

I previously worked around SAP HR-related business processes and wanted to revisit that experience by rebuilding a small but realistic workflow on my own.

Instead of trying to reproduce a full HR system, this project focuses on a narrow and practical flow:

- An employee submits a leave request
- An approver reviews the request
- The request is approved or rejected
- Leave balance is reduced only after approval

## Purpose

- Reorganize and revisit SAP HR-like business flow
- Build a business object with RAP
- Create list/detail/create UI with SAP Fiori elements
- Turn a small but realistic workflow into a portfolio project

## Planned Features

- Employee master list
- Leave request creation
- Request list display
- Request detail display
- Approve / Reject
- Leave balance validation
- Duplicate request validation
- Status management

## Business Rules

- Request cannot be submitted if leave balance is insufficient
- Request cannot be submitted if start date is after end date
- Duplicate requests for the same employee and same date are not allowed
- Reject reason is mandatory when rejecting
- Leave balance is reduced only when the request is approved
- Rejected or cancelled requests do not reduce leave balance

## Tech Stack

- SAP BTP ABAP Environment / ABAP Platform
- ABAP RAP
- CDS View Entity
- Behavior Definition / Behavior Implementation
- OData Service Binding
- SAP Fiori elements

In RAP, a service binding is used to expose services through OData and to launch Fiori Elements App Preview. UI annotations in CDS can be used to control the Fiori Elements UI.  [oai_citation:3‡SAP](https://developers.sap.com/tutorials/abap-environment-restful-programming-model..html?utm_source=chatgpt.com)

## Planned UI

1. Employee List
2. Leave Request List Report
3. Leave Request Object Page
4. Create Leave Request
5. Approve / Reject Action

## Data Model Overview

### Employee
- Employee ID
- Name
- Department
- Approver ID
- Remaining Paid Leave Balance

### Leave Request
- Request ID
- Employee ID
- Leave Type
- Start Date
- End Date
- Requested Days
- Reason
- Status
- Reject Reason
- Approver ID
- Created At
- Updated At

### Leave Type
- Leave Type Code
- Name
- Deduction Flag

## Future Enhancements

- Half-day leave
- Holiday / non-working day calculation
- Workflow enhancement
- Authorization control
- Draft support
- Launchpad deployment

The ABAP environment provides access to SAP Fiori applications and Fiori Launchpad capabilities.  [oai_citation:4‡SAPヘルプポータル](https://help.sap.com/docs/sap-btp-abap-environment/abap-environment/ui-development-overview?locale=ja-JP&utm_source=chatgpt.com)

## What this repository demonstrates

- Understanding of SAP-style business processes
- Ability to narrow requirements into a realistic MVP
- RAP-based business application design
- Fiori-based list/detail/create experience
- Portfolio-ready technical documentation
