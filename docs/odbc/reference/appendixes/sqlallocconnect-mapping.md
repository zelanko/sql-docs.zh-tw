---
title: SQLAllocConnect 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065018"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 對應
當應用程式呼叫**SQLAllocConnect**透過 ODBC 3。*x*驅動程式，會呼叫**SQLAllocConnect**(*henv*， *phdbc*) 會對應至**SQLAllocHandle** ，如下所示：  
  
1.  驅動程式管理員配置的連接，並傳回應用程式。  
  
2.  當應用程式建立連接時，驅動程式管理員會呼叫  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在將驅動程式與*InputHandle*設為*henv*，並*OutputHandlePtr*設定為*phdbc*。
