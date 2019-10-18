---
ms.openlocfilehash: 0aeb87de6526b345a97c4ae57a45e423a283490e
ms.sourcegitcommit: 65e9a0388cec4abe69bfc1c5890afdd418a22304
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72261736"
---
Bu modülde kimlik doğrulaması için OpenID Connect kavramlarını incelediniz.

Bir örnek uygulamadan yararlanarak kullanıcıların tek bir Azure Active Directory (Azure AD) kiracısından oturum açması için OpenID Connect ASP.NET OWIN ara yazılımını kullandınız. Kullanıcılar artık Office 365'te kullandıkları aynı hesaplarla oturum açıyor.

## <a name="clean-up"></a>Temizleme

Bu modülü bitirdiğinizde korumalı alan kaynaklarınızı otomatik olarak temizler. Ama oluşturduğunuz Azure AD kiracısının el ile silinmesi gerekir.

Azure AD kiracısını silmek için şu adımları izleyin:

1. [Azure portalının](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) üst çubuğunda hesabınızı seçin ve sonra da **Dizini değiştir**'i seçin.
1.  4\. ünitede oluşturduğunuz **Learn Module AAD Tenant** dizinini seçin.
1. Sol bölmede **Azure Active Directory**'yi seçin, ardından **Uygulama Kayıtları**'nı ve **WebApp-OpenIDConnect-DotNet** kaydını seçin.
1. **Sil**'i ve sonra da **Evet**'i seçin.
1. Sol bölmede **Azure Active Directory**’yi seçin. **Yönet**'in altında **Özellikler**'i seçin.
1. **Azure kaynakları için erişim yönetimi**'nin altında **Evet**'i ve sonra da **Kaydet**'i seçin.
1. Portalın sağ üst kısmında kullanıcı hesabınızı seçin ve sonra da **Oturumu kapat**'ı seçin.
1. Normal kimlik bilgilerinizle oturum açın. Üst çubukta hesabınızı seçin ve sonra da **Dizini değiştir**'i seçin.
1.  4\. ünitede oluşturduğunuz **Learn Module AAD Tenant** dizinini seçin.
1. Sol bölmede **Azure Active Directory**'yi seçin, **Dizini sil**'i seçin ve **Sil**'i seçin.
1. Portalın sağ üst kısmında kullanıcı hesabınızı seçin ve sonra da **Oturumu kapat**'ı seçin.

## <a name="further-reading"></a>Daha fazla bilgi

- [OpenID Connect ve Azure Active Directory kullanarak web uygulamalarına erişim yetkisi verme](https://docs.microsoft.com/azure/active-directory/develop/v1-protocols-openid-connect-code)
- [OpenID Connect belirtimi](https://openid.net/specs/openid-connect-core-1_0.html)
- [Kimlik belirteçleri](https://docs.microsoft.com/azure/active-directory/develop/id-tokens)
- [Azure Active Directory erişim belirteçleri](https://docs.microsoft.com/azure/active-directory/develop/access-tokens)
