---
title: 答案是 ODBC 嗎？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288089"
---
# <a name="is-odbc-the-answer"></a>答案是 ODBC 嗎？
在深入探討互操作性問題之前,請考慮以下問題:應用程式是否應使用ODBC? 在 ODBC 指南中,這似乎是一個奇怪的問題,但事實上,這是一個合理的問題。 ODBC 並非旨在完全替換本機資料庫 API,也不是旨在在所有情況下提供資料庫存取。 它旨在為資料庫提供一個通用介面,旨在使應用程式程式員不必瞭解和維護到多個資料庫的連結。  
  
 自定義應用程式是本機資料庫 API 的主要候選項。 主要原因是自定義應用程式通常使用單個 DBMS,並且不需要互通。 本機資料庫 API 在公開特定 DBMS 的功能方面可能比 ODBC 做得更好,並且可能會公開 ODBC 未公開的功能。 此外,由於自定義應用程式的開發人員通常熟悉其 DBMS 的本機資料庫 API,因此幾乎沒有理由學習 ODBC。 但是,值得注意的是,對於某些 DBMS,ODBC 是本機資料庫 API。  
  
 那麼,哪些應用程式是 ODBC 的候選應用程式? 最佳候選是使用多個 DBMS 的應用程式。 這包括幾乎所有通用和垂直應用程式。 它還包括許多自定義應用程式。 例如,使用多個不同 DBMS 的自訂應用程式與多個本機 API 相比,使用 ODBC 編寫起來要容易得多、更簡潔。 當公司從一個 DBMS 移動到另一個 DBMS 或針對不同的 DBMS 部署同一應用程式時,使用 ODBC 編寫的自定義應用程式更易於遷移。
