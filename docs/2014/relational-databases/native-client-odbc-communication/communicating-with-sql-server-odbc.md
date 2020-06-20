---
title: 與 SQL Server 通訊（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: rothja
ms.author: jroth
ms.openlocfilehash: c41ac2dcce9c5bdbdd351148d16bcaa8f067d22f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021203"
---
# <a name="communicating-with-sql-server-odbc"></a>與 SQL Server 進行通訊 (ODBC)
  若要讓 ODBC 應用程式與的實例進行通訊 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，它必須配置環境和連接控制碼，並連接到資料來源。 建立連接之後，應用程式可以將查詢傳送到伺服器，並處理任何結果集。 當應用程式使用資料來源完畢時，它會中斷與資料來源的連接，並釋出連接控制代碼。 當應用程式釋出其所有連接控制代碼時，它會釋出環境控制代碼。  
  
 應用程式可以連接到任何數目的資料來源。 應用程式可以使用驅動程式與資料來源的組合、相同的驅動程式與資料來源組合，甚至相同驅動程式與相同資料來源的多個連接。  
  
 您可以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從 MSDN 上的[SQL Server 下載](https://go.microsoft.com/fwlink/?LinkId=62796)] 頁面下載 Native Client ODBC 範例。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [配置環境控制代碼](allocating-an-environment-handle.md)  
  
-   [配置連接控制代碼](allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 資料來源](../../integration-services/connection-manager/data-sources.md)  
  
-   [連接到 &#40;ODBC&#41;的資料來源](connecting-to-a-data-source-odbc.md)  
  
-   [從資料來源中斷連接](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
