---
title: Administración extensible de claves (EKM) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 9115535ecc2569e035f4831589e53191e2634f61
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957408"
---

#### <a name="other-types-of-ekm-device-specific-authentication"></a>Otros tipos de autenticación específicas del dispositivo EKM  
 Para aquellos módulos EKM que usan una autenticación que no sea la Windows o la de una combinación de *nombre de usuario/contraseña* , la autenticación se debe realizar independientemente de
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>Cifrado y descifrado por parte de un dispositivo EKM  
 Puede utilizar las siguientes funciones y características para cifrar y descifrar datos utilizando claves simétricas y asimétricas:  
  
|Función o característica|Referencia|  
|-------------------------|---------------|  
|Cifrado de claves simétricas|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Cifrado de claves asimétricas|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, "texto_no_cifrado", ...)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(texto_cifrado, ...)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey (key_guid, 'texto no cifrado')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(texto cifrado)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>Cifrado de claves de la base de datos mediante claves EKM  
 pueden utilizar claves EKM para cifrar otras claves de una base de datos. Puede crear y utilizar tanto claves simétricas como asimétricas en un dispositivo EKM. Puede cifrar claves simétricas nativas (no EKM) con claves asimétricas EKM.  
  
 El ejemplo siguiente crea una clave simétrica de la base de datos y la cifra utilizando una clave de un módulo EKM.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
