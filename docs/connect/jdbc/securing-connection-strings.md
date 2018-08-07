---
title: 保護連接字串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 69ce8557-5260-4ea4-81b8-d0c5481f0868
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b13501bac840f2f39390a3cfed184c11dc9f36bf
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453122"
---
# <a name="securing-connection-strings"></a>保護連接字串的安全

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

保護資料來源的存取，是協助保護應用程式安全的其中一個最重要目標。 若要限制存取資料來源，您必須採取預防措施，以協助保護連接資訊 (例如使用者識別碼、密碼和資料來源名稱) 的安全。 將使用者識別碼和密碼存成純文字 (例如原始程式碼中) 會造成嚴重的安全性問題。 即使您在外部來源中提供編譯版本的程式碼 (其中含有使用者識別碼和密碼資訊)，編譯過的程式碼仍有可能被反組譯因而暴露使用者識別碼和密碼。 因此，請務必遵守不要在程式碼中加入任何重要資訊，例如使用者識別碼和密碼。

建議您不要在應用程式原始程式碼中，一起儲存密碼和連線 URL。 而是應將密碼儲存在具有限制存取權限的單獨檔案中。 該檔案的存取權限可以授與給執行應用程式的內容。

另一個方法是在檔案中儲存加密的密碼。 請確定所使用的加密 API 不需要在某處儲存金鑰，而且不是從使用者密碼所衍生出來的。 例如，可以考慮使用憑證型的公開/私密金鑰組，或使用的方法是雙方使用金鑰協定 (Diffie-Hellman 演算法)，針對加密產生相同的祕密金鑰，而不需要傳輸祕密金鑰。

如果會從外部來源取得連接字串資訊 (例如由使用者提供使用者識別碼和密碼)，您必須驗證該來源的任何輸入，以確定這些輸入遵從正確的格式並且不含會影響連接的其他參數。

## <a name="see-also"></a>另請參閱

[保護 JDBC Driver 應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)
