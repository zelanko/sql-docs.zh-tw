---
title: "驗證使用者輸入 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f46806c35bffcc9cacd77483f6a4cfe01153d5a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="validating-user-input"></a>驗證使用者輸入
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您建構存取資料的應用程式時，您應該假設所有使用者輸入都是惡意的，直到經過證明為止。 如果無法證明，這可能會讓您的應用程式容易受到攻擊。 一種可能的攻擊類型稱為 SQL 資料隱碼，其中惡意程式碼會加入到稍後傳遞到的執行個體的字串[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]剖析與執行。 若要避免這類型的攻擊，您應該搭配參數 (如有可能) 使用預存程序，並永遠驗證使用者輸入。  
  
 在用戶端程式碼中驗證使用者輸入相當重要，如此您不會浪費與伺服器的往返。 在伺服器上驗證預存程序的參數以捕捉無效的輸入以及略過用戶端驗證的輸入也同等重要。  
  
 多個 SQL 資料隱碼以及如何避免這樣的詳細資訊，請參閱 < SQL 資料隱碼 」 中,[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。 如需有關驗證預存程序參數的詳細資訊，請參閱 「 預存程序 ([!INCLUDE[ssDE](../../includes/ssde_md.md)]) 」 以及從屬主題中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [保護 JDBC 驅動程式應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
