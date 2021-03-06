AppDF File Structure
-------------

An AppDF file is a ZIP archive where all the files describing the application are collected. Here is an example of a simple AppDF file content:
```
description.xml
Life.apk
icon.png
screenshot01.png
screenshot02.png
screenshot03.png
screenshot04.png
```

As you see there are just few files: APK file, application icon, screenshot and description.xml file that contains all the information about the application (title, description, category, parental control info, requirements, etc). 

Let's consider more advanced example of AppDF package:
```
description.xml
description_fr.xml
description_de.xml
description_kr.xml
Life_ics.apk
Life_fro.apk
images/icon114x114.png
images/icon135x135.png
images/icon512x512.png
images/en/screenshot01_en.png
images/en/screenshot02_en.png
images/en/screenshot03_en.png
images/en/screenshot04_en.png
images/en/largepromo_en.png
images/en/smallpromo_en.png
images/fr/screenshot01_fr.png
images/fr/screenshot02_fr.png
images/fr/screenshot03_fr.png
images/fr/screenshot04_fr.png
images/fr/largepromo_fr.png
images/fr/smallpromo_fr.png
images/de/screenshot01_de.png
images/de/screenshot02_de.png
images/de/screenshot03_de.png
images/de/screenshot04_de.png
images/en/screenshot01_kr.png
images/en/screenshot02_kr.png
images/en/screenshot03_kr.png
images/en/screenshot04_kr.png
images/en/largepromo_de.png
images/en/smallpromo_de.png
images/en/largepromo_kr.png
images/en/smallpromo_kr.png
```

As you can see the application could include several APK files, the images and description could support localization and different stores require different resolution for the app icon.  Although the AppDF will automatically rescale your images to needed format if you want fine tuning you could prefer to include several sizes for the images.

The only naming convention for the files inside AppDF package is that the description XML file should be called `description.xml`. You can include all localizations to the `description.xml` file or place them into separate files whos name should have form of `description_XXXX.xml`. Where XXXX could be any suffix. These additional files should have `<description>` as a root tag. The system will automatically merge all such files into one. Using these additional files is optional, you can easily include all the localizations in one `description.xml` file. All other files could have any names supported by ZIP, could be placed in the top folder or in any of the subfolders. The names of the additional files are defined in the `description.xml` file.

Sample Description.xml File
-------------

```xml
<?xml version="1.0" encoding="UTF-8"?>

<application-description-file version="1">

<application package="ru.yandex.shell">

  <categorization>
    <!--Options: application, game-->
    <type>application</type>
    <!--See the list of AppDF categories and subcategories in the documentation-->
    <category>finance</category>
    <subcategory>investing</subcategory>
  </categorization>

  <!--Language is set in two letter ISO 639-1 codes, default is an optional attribute, if set this information is used for other languages where a particular native text is missed-->
  <description language="en" default="yes">
    <!-- Maximum length of title: 30 symbols-->
    <title>Yandex.Shell</title>
    <keywords>shell, homescreen, launcher</keywords>
    <!--If several versions of short-description tag are presented the store will take the longest-->
    <short-description>My short description</short-description>
    <short-description>Slightly longer version of my short description</short-description>
    <short-description>Even more longer version of my short description text</short-description>
    <full-description>My full description here</full-description>
	<!--Optional tag. You can include full description with HTML markup for those stores that support such description-->
    <full-description html="yes">My full description here</full-description>
	<!--Optional tag. You can include full description without list of feeatures. It will be used by those stores that support separate feature list tag-->
    <full-description featureless="yes">My full description here</full-description>
	<!--Will be used only be some stores, most of the stores do not use this tag-->
    <features>
      <feature>New dialer</feature>
      <feature>Home screen</feature>
      <feature>3D interface</feature>
    </features>
    <recent-changes>It is a description of what was changed in the latest version</recent-changes>

    <!--Optional tag, some stores require it for apps that collect personal information-->
    <privacy-policy>http://legal.yandex.com/privacy/</privacy-policy>

    <!--Optional tag, if presented it give custom EULA that some stores will show before installation-->
    <eula></eula>

    <images>
	  <!--Appp icon should have 512x512 size-->
      <app-icon size="512">icon.png</app-icon>
	  <!--Optionally you could include application icon in different sizes. If missed AppDF will automatically resize your icon-->
      <app-icon size="135">icon_135x135.png</app-icon>
      <app-icon size="144">icon_144x144.png</app-icon>
      <large-promo>promo.png</large-promo>
      <small-promo>feature.png</small-promo>
      <!--Minimum two screenshots should be presented-->
	  <screenshots>
        <screenshot>screenshot01_en.png</screenshot>
        <screenshot>screenshot02_en.png</screenshot>
        <screenshot>screenshot03_en.png</screenshot>
        <screenshot>screenshot04_en.png</screenshot>
        <screenshot>screenshot05_en.png</screenshot>
      </screenshot>
    </images>

    <youtube-video>x8723jw2KL</youtube-video>
    <video-file>video1.mp4</video-file>

  </description>

  <description language="ru">
    <title>Яндекс.Shell</title>

    <images>
      <screenshot>screenshot01_ru.png</screenshot>
      <screenshot>screenshot02_ru.png</screenshot>
      <screenshot>screenshot03_ru.png</screenshot>
    </images>

  </description>


  <content-description>
    <!--Minimum age according to ESRB rating system--> 
    <content-rating>12</content-rating>

    <rating-certificates>
      <!--Possible values are 3, 7, 12, 16, 18. "certificate" attribute is optional-->
      <rating-certificate type="PEGI" certificate="whirl-pegi.pdf">7</rating-certificate>
      <!--Possible values are 3, 6, 10, 13, 17, 18. "certificate" attribute is optional-->
      <rating-certificate type="ESRB" certificate="whirl-esrb.pdf">7</rating-certificate>
      <!--Possible values are "all", 12 15, 18. "certificate" attribute is optional-->
      <rating-certificate type="GRB" certificate="whirl-gbr.pdf">all</rating-certificate>
      <!--Possible values are "all", 12, 15, 17, 18. "certificate" attribute is optional-->
      <rating-certificate type="CERO" certificate="whirl-cero.pdf">all</rating-certificate>
      <!--Possible values are "l", 10, 12, 14, 16, 18. "certificate" attribute is optional-->
      <rating-certificate type="DEJUS" certificate="whirl-dejus.pdf" mark="dejus_mark.jpg">l</rating-certificate>
      <!--Possible values are 0, 6, 12, 16, 18. "certificate" attribute is optional-->
      <rating-certificate type="FSK" certificate="whirl-fsk.pdf">0</rating-certificate>
    </rating-certificates>
    <!--All sub-tags are required, possible options are "no", "light", "strong"-->
    <content-descriptors>
      <cartoon-violence>no</cartoon-violence>
      <realistic-violence>no</realistic-violence>
      <!--May contain profanity, sexual innuendo, threats, and all manner of slurs and epithets.-->
      <bad-language>no</bad-language>
      <!--May contain scenes that are considered too disturbing or frightening to younger or more emotionally vulnerable players.-->
      <fear>light</fear>
      <!--Sexual and suggestive content. May contain references to sexual attraction or sexual intercourse. Also may contain nudity and characters dressed in suggestive clothing.-->
      <sexual-content>no</sexual-content>
      <!--May contain references to illegal drugs or a fictional substance that has parallels to real-life illegal drugs (in use, possession, or sale).-->
      <drugs>no</drugs>
      <!--May contain elements that encourage or teach gambling.-->
      <gambling-refference>no</gambling-refference>
      <!--May contain references to alcohol-->
      <alcohol>no</alcohol>
      <!--May contain references to smoking or tobacco-->
      <smoking>strong</smoking>
      <!--May contain cruelty or harassment based on race, ethnicity, gender, or sexual preferences.-->
      <discrimination>no</discrimination>
    </content-descriptors>
	<included-activities>
      <in-app-billing>no</in-app-billing>
      <gambling>no</gambling>
      <advertising>no</advertising>
      <user-generated-content>no</user-generated-content>
      <user-to-user-communications>no</user-to-user-communications>
      <account-creation>no</account-creation>
      <personal-information-collection>no</personal-information-collection>
	</included-activities>
  </content-description>

  <availability>
    <!--Optional tag, if missed all the countries are included-->
    <countries>
      <!--Two symbol ISO 3166-1 country code -->
      <include>en</include>
      <include>ru</include>
      <exclude>de</exclude>
    <countries>

    <!--Optional tag, if missed the app become available immediatly without experiation date-->
    <period>
      <!--Optional tag, if missed the app become available immediatly -->
      <since year="2012" month="12" day="23"/>
      <!--Optional tag, if missed the app is without experiation date-->    
      <until year="2013" month="12" day="23"/>
    </period>
  </availability>	

  <!--If free attribute is set to "yes" then all the subtags except <trial-version> are ignored. -->
  <!--If app is not free then "base-price" is required. currency is set in three cappital letter ISO 4217 currency code -->
  <!--local-price tags are optional, if set they define local prices. Country is set in two letter ISO 3166-1 country code, currency is set in three cappital letter ISO 4217 currency code-->
  <!--Dot not comma should be used as decimal dilimiter symbol-->
  <price free="yes">
    <base-price currency="USD">4.95</base-price>
    <local-price country="de" currency="EUR">3.95</local-price>
    <local-price country="fr" currency="EUR">3.95</local-price>
    <local-price country="ru" currency="RUB">99</local-price>
    <!--Available for free apps only. Set to "yes" if this application is a trial version of another application. Optional attribute full-version defines package name of the corresponding full version-->
    <trial-version full-version="com.yandex.shellfullversion"/>
  </price>

  <apk-files>
    <apk-file>yandexshell2.apk</apk-file>
    <apk-file>yandexshell3.apk</apk-file>
    <apk-file-with-extnsion>
	  <apk-file>yandexshell4.apk</apk-file>
	  <extension>extensionfile.zip</extension>
	</apk-file-with-extnsion>
  </apk-files>

  <!--Optional tag, add it if the application has some special requirements-->
  <requirements>
    <features>
      <!--Optional tag, set to yes, if your application requires root access-->
      <root>no</root>
      <!--Optional tag, set to yes, if your application requires Google Mobile Services, will dramatically limit supported stores-->
      <gms>no</gms>
    </features>

    <!--Optional tag, if missed this information is taked from the APK files. All languages are defined by their two letter ISO 639-1 language codes-->
    <supported-languages>
      <language>en</language>
      <language>ru</language>
      <language>de</language>
      <language>fr</language>
      <language>it</language>
    </supported-languages>

    <!--Optional tag, if missed information about the supported devices is taken from the APK file. Use this tag if you want to add some exceptions-->
    <supported-devices>
      <exclude>kyleopen</exclude>
      <exclude>SHW-M130K</exclude>
    </supported-devices>

    <!--Optional tag, if missed information about the supported screen resolutions is taken from the APK file. Use this tag if you want to add some exceptions-->
    <supported-resolutions>
      <exclude>480x856</exclude>
      <include>240x400</include>
    </supported-resolutions>
  </requirements>

  <!--Optional tag that collects some store specific information-->
  <!--Top level subtags correspond to store ids, see the documentation for the list of these ids-->
  <!--The store tags could also include replacement of any of the subtags from the <application> tag. See -->
  <store-specific>
    <amazon>
      <!--Options: phone, tablet, all-->
      <form-factor>all</form-factor>
      <!--Optional tag, default value is no-->
      <free-app-of-the-day-eligibility>yes</free-app-of-the-day-eligibility>
      <apply-amazon-drm>yes</apply-amazon-drm>
      <kindle-support>
        <kindle-fire-first-generation>yes</kindle-fire-first-generation>
        <kindle-fire>yes</kindle-fire>
        <kindle-fire-hd>yes</kindle-fire-hd>
        <kindle-fire-hd-8-9>yes</kindle-fire-hd-8-9>
      </kindle-support>
      <binary-alias>Version 1</binary-alias>
    </amazon>
    <samsung>
      <!--Options: tv, phone, tablet, or any combination in comma separated string-->
      <form-factor>phone,tablet</form-factor>
      <!--Optional tag, set to yes, if your application uses Samsung Zirconia DRM protection-->
      <contains-zirconia-protection>yes</contains-zirconia-protection>
      <!--Optional tag, set to yes, if your application requires Samsung S-Pen-->
      <s-pen>yes</s-pen> 
      <!-- Samsung requires each app to have 2-5 tags -->
      <tags>
        <tag>Education / Video</tag>
        <tag>Music / Album</tag>
      </tags>
    </samsung>
    <slideme>
      <!--Optional tag, if missed the license is considered as proprietary-->
	  <license-type>apache2</license-type>
    </slideme>
  </store-specific>

  <!--Special requirements to test your app. maximum characters in case of Amazon: 4000-->
  <testing-instructions>
  </testing-instructions>

  <!--You must include these tags in order to confirm your agreement with the corresponding agreement-->
  <consent>
    <!--http://play.google.com/about/developer-content-policy.html-->
    <google-android-content-guidelines>yes</google-android-content-guidelines>
    <!--https://support.google.com/googleplay/android-developer/support/bin/answer.py?hl=en&answer=113770-->
    <us-export-laws>yes</us-export-laws>
  </consent>

  <!--Optional tag, if missed customer support info from the account is used-->
  <customer-support>
    <phone>+1 (555) 1234-56-78</phone>
    <email>support@yandex-team.ru</email>
    <website>http://www.yandex.ru/support</website>
  </customer-support>

</application>

</application-description-file>
```

Description.xml Structure
-------------

Table of Contents:
* [categorization](#categorization)
	* [type](#categorizationtype)
	* [category](#categorizationcategory)
	* [subcategory](#categorizationsubcategory)
* [description](#description)
	* [title](#descriptiontitle)
	* [keywords](#descriptionkeywords)
	* [short-description](#descriptionshort-description)
	* [full-description](#descriptionfull-description)
	* [features](#descriptionfeatures)
	* [recent-changes](#descriptionrecent-changes)
	* [privacy-policy](#descriptionprivacy-policy)
	* [eula](#descriptioneula)
	* [images](#descriptionimages)
		* [app-icon](#descriptionimagesapp-icon)
		* [large-promo](#descriptionimageslarge-promo)
		* [small-promo](#descriptionimagessmall-promo)
		* [screenshots](#descriptionimagesscreenshots)
	* [youtube-video](#descriptionyoutube-video)
	* [video-file](#descriptionvideo-file)
* [content-description](#content-description)
	* [content-rating](#content-descriptioncontent-rating)
	* rating-certificates
		* [rating-certificate](#content-descriptionrating-certificatesrating-certificate)
	* [content-descriptors](#content-descriptioncontent-descriptors)
	* [included-activities](#content-descriptionincluded-activities)
* [availability](#availability)
	* [countries](#availabilitycountries)
	* period
		* [since](#availabilityperiodsince)
		* [until](#availabilityperioduntil)
* [price](#price)
	* [base-price](#pricebase-price)
	* [local-price](#pricelocal-price)
	* [trial-version](#pricetrial-version)
* [apk-files](#apk-files)
* [requirements](#requirements)
	* [features](#requirementsfeatures)
		* [root](#requirementsroot)
		* [gms](#requirementsgms)
	* [supported-languages](#requirementssupported-languages)
	* [supported-devices](#requirementssupported-devices)
	* [supported-resolutions](#requirementssupported-resolutions)
* [store-specific](#store-specific)
	* [amazon](#store-specificamazon)
	* [samsung](#store-specificsamsung)
	* [slideme](#store-specificslideme)
* [testing-instructions](#testing-instructions)
* [consent](#consent)
* [customer-support](#customer-support)
	* [phone](#customer-supportphone)
	* [email](#customer-supportemail)
	* [website](#customer-supportwebsite)


### categorization

Example:
```xml
<categorization>
  <type>application</type>
  <category>finance</category>
  <subcategory>investing</subcategory>
</categorization>
```

#### categorization/type

Required. No attributes. Value could be either `application` or `game`.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Possible values</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Categorization / Application Type</td>
    <td>Yes</td>
    <td>Applications, Games</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Category</td>
    <td>Yes</td>
    <td>Games is one item in the application category list</td>
  </tr>
  <tr>
    <td>Opera Mobile Store</td>
    <td>Yes</td>
    <td>Category</td>
    <td>Yes</td>
  </tr>
</table>

#### categorization/category

Required. No attributes. AppDF format has its own list of categories for both games and applications. This category list is developed to be easily mapped to any of the application store category lists.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Categorization / Category</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Category</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Opera Mobile Store</td>
    <td>Yes</td>
    <td>Category</td>
    <td>Yes</td>
  </tr>
</table>

#### categorization/subcategory

Required. 
No attributes. 

Although some stores don't use subcategories AppDF includes as detailed category information as possible. It is always easy to broaden detailed AppDF category+subcategory information to a less detailed particular store category list.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Category</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Opera Mobile Store</td>
    <td>Yes</td>
    <td>Category</td>
    <td>Yes</td>
  </tr>
</table>

### description 
Required.
Attributes: `language`, `default`. 

This section contains product in text form as well as pictures and videos. There could be several `<description>` tags for different languages. One of the `<description>` tags should be default (`default=yes`). If some information is missed in the localized versions of the `<description>` tag it will be taken from the default language.

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
  </tr>
  <tr>
    <td>language</td>
    <td>two letter ISO 639-1 language code (like "en") or two letters language code + two letter ISO 3166‑1 country code (like "en-us")</td>
    <td>required tag</td>
  </tr>
  <tr>
    <td>default</td>
    <td>yes, no</td>
    <td>no</td>
  </tr>
</table>

Example:
```xml
<description language="en" default="yes">
  <title>Yandex.Shell</title>
  <keywords>shell, homescreen, launcher</keywords>
  <short-description>My short description</short-description>
  <short-description>Slightly longer version of my short description</short-description>
  <short-description>Even more longer version of my short description text</short-description>
  <full-description>My full description here</full-description>
  <full-description html="yes">My full description here</full-description>
  <full-description featureless="yes">My full description here</full-description>
  <features>
    <feature>New dialer</feature>
    <feature>Home screen</feature>
    <feature>3D interface</feature>
  </features>
  <recent-changes>It is a description of what was changed in the latest version</recent-changes>
  <x-opera-app-registration-instructions>Sample text here</x-opera-app-registration-instructions>

  <privacy-policy>http://legal.yandex.com/privacy/</privacy-policy>
  <eula></eula>

  <images>
    <app-icon size="512">icon.png</app-icon>
    <app-icon size="135">icon_135x135.png</app-icon>
    <app-icon size="144">icon_144x144.png</app-icon>
    <large-promo>promo.png</large-promo>
    <small-promo>feature.png</small-promo>
    <screenshots>
      <screenshot>screenshot01_en.png</screenshot>
      <screenshot>screenshot02_en.png</screenshot>
      <screenshot>screenshot03_en.png</screenshot>
      <screenshot>screenshot04_en.png</screenshot>
      <screenshot>screenshot05_en.png</screenshot>
    </screenshots>
  </images>

  <youtube-video>x8723jw2KL</youtube-video>
  <video-file>video1.mp4</video-file>

</description>
```

#### description/title

Required. 
No attributes. 
Maximum length: 30.

Application name, shown in the application list. As everything in the `<description>` section is can be localized.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Product Details / Title</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>30</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Description / Display Title</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>250</td>
  </tr>
  <tr>
    <td>Opera Mobile Store</td>
    <td>Yes</td>
    <td>Title</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Unlimited</td>
  </tr>
</table>

#### description/keywords

Required. 
No attributes. 

Comma separated list of keywords.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Description / Keywords</td>
    <td>No</td>
    <td>Yes</td>
    <td>80</td>
    <td></td>
  </tr>
</table>

#### description/short-description

Required. 
No attributes. 
Maximum length: at least one tag should be shorter than 80 symbols.

Short application description used in the app lists next to the app title. Some stores include such short description to the lists, some do not. Different stores have different requirements for maximum short description length. In order to have flexibility to get the best from each of the stores you can include several copies of short description tag. The store will take the longest one that is fits in its maximum size.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Product Details / Promo Text</td>
    <td>No</td>
    <td>Yes</td>
    <td>80</td>
    <td>Is not shown in the app list but only on promotion pages</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Description / Short description</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>1200</td>
    <td>A shorter version of your app description for use on mobile devices.</td>
  </tr>
</table>

#### description/full-description

Required. 
Attributes: `html`, `featureless`. 
Maximum length: 4000.


Full application description shown on the product page. You can include several copies of your application description, one with HTML markup and one without. The stores will use one of these descriptions depending on do they support HTML in the description field or not. In the same way you can include description with included feature list and one without. The one without will be used for the stores that use a separate feature list (to avoid feature list duplication).

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>html</td>
    <td>yes,no</td>
    <td>no</td>
    <td></td>
  </tr>
  <tr>
    <td>featureless</td>
    <td>yes, no</td>
    <td>no</td>
    <td></td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
    <th>Markup support</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Product Details / Title</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>4000</td>
    <td>simple HTML, no links</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Description / Long description</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>4000</td>
    <td>simple HTML, no links</td>
  </tr>
</table>

#### description/features
Optional.
No attributes.

Some stores support separate feature list (most assumes that the feature list is included into the full description). Each `<feature>` subtag should contain one feature description.

Example:
Example:
```xml
<features>
  <feature>New dialer</feature>
  <feature>Home screen</feature>
  <feature>3D interface</feature>
</features>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Description / Product feature bullets</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Unlimited</td>
  </tr>
</table>

#### description/recent-changes

Optional. 
No attributes. 
Maximum length: 500.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Maximum length</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Product Details / Recent changes</td>
    <td>No</td>
    <td>Yes</td>
    <td>500</td>
    <td>Describes the changes of the latest version (version number is taken from APK file)</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

#### description/privacy-policy
Optional. 
No attributes. 

Link to a webpage with your privacy policy for this application.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Privacy Policy / Link to policy</td>
    <td>No</td>
    <td>No</td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Privacy policy URL</td>
    <td>No</td>
    <td>No</td>
    <td>Privacy policy URL</td>
  </tr>
</table>

#### description/eula

Optional. 
No attributes. 

Link to a webpage with your End User License Agreement for this application.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

#### description/images

This tag contains all application image assets. As everything inside the `<description>` tag it can be localized. If a localized version of the `<description>` tag does not contains one of the four sections then images from the default languages are taken. So you need to include only those images that are actually localized into the localized versions of the `<description>` tag and do not need to repeat the images that are the same as in the default language.  

Example:
```xml
<images>
  <app-icon size="512">icon.png</app-icon>
  <app-icon size="135">icon_135x135.png</app-icon>
  <app-icon size="144">icon_144x144.png</app-icon>
  <large-promo>promo.png</large-promo>
  <small-promo>feature.png</small-promo>
  <screenshots>
    <screenshot>screenshot01_en.png</screenshot>
    <screenshot>screenshot02_en.png</screenshot>
    <screenshot>screenshot03_en.png</screenshot>
    <screenshot>screenshot04_en.png</screenshot>
    <screenshot>screenshot05_en.png</screenshot>
  </screenshots>
</images>
```

##### description/images/app-icon

Required. 
Attributes: `size`. 

High resolution application icon. Different stores require different resolutions of this icon. You can include several versions of the `<app-icon>` tag with different `size` attributes. The store will automatically select right size. AppDF will automatically rescale your image if there is no needed size. Most of the stores use 512x512 PNG image, so it is highly recommended to include such version.

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>size</td>
    <td>a number</td>
    <td>512</td>
    <td></td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Resolution</th>
    <th>Formats</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Graphic Assers / High-res icon</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>512x512</td>
    <td>32-bit PNG (with alpha)</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Images & Multimedia / Small Icon, Large icon</td>
    <td>Yes</td>
    <td>No</td>
    <td>114x114 + 512x512</td>
    <td>PNG (with transparency)</td>
  </tr>
</table>

##### description/images/large-promo
Optional. 
No attributes. 

Large promotion picture usually used by the stores on the PC websites. 


<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Resolution</th>
    <th>Formats</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Graphic Assers / Feature Graphic</td>
    <td>No</td>
    <td>Yes</td>
    <td>1024x500</td>
    <td>JPG or 24-bit PNG (no alpha)</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Images & Multimedia / Promotional image</td>
    <td>No</td>
    <td>No</td>
    <td>1024x500</td>
    <td>PNG or JPG</td>
  </tr>
</table>

##### description/images/small-promo

Optional. 
No attributes. 

Small promotion picture usually used by the stores on a mobile device for promoted apps. 


<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Resolution</th>
    <th>Formats</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Graphic Assers / Feature Graphic</td>
    <td>No</td>
    <td>Yes</td>
    <td>180x120</td>
    <td>JPG or 24-bit PNG (no alpha)</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>PNG or JPG</td>
  </tr>
</table>

##### description/images/screenshots
Required. 
No attributes. 

Contains several `<screenshot>` subtags. Each `<screenshot>` subtag describes one screenshot. Different stores use different number of screenshots. You should provide at least four screenshots to support all the stores. If you provide more screenshots than a store can use the first screenshots are used. 

Example:
```xml
<screenshots>
  <screenshot>screenshot01_en.png</screenshot>
  <screenshot>screenshot02_en.png</screenshot>
  <screenshot>screenshot03_en.png</screenshot>
  <screenshot>screenshot04_en.png</screenshot>
  <screenshot>screenshot05_en.png</screenshot>
</screenshots>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Resolution</th>
    <th>Formats</th>
    <th>Number</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Graphic Assers / Screenshots</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>320x480, 480x800, 480x854, 1280x720, 1280x800</td>
    <td>JPG or 24-bit PNG (no alpha)</td>
    <td>2+</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Images & Multimedia / Screenshots</td>
    <td>Yes</td>
    <td>No</td>
    <td>800x480, 1024x600, 1280x720, 1280x800, or 1920x1200 (portrait or landscape)</td>
    <td>JPG or PNG</td>
    <td>3-10</td>
  </tr>
</table>

#### description/youtube-video

Optional. 
No attributes. 

If you have a video about your product at YouTube you can include it here. Please include only ID not entire URL. For example if your YouTube video URL is:
https://www.youtube.com/watch?v=4YcBHQ2fCDE

then tag value should be just `4YcBHQ2fCDE`. Like:
```xml
<youtube-video>4YcBHQ2fCDE</youtube-video>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Graphic Assets / Promo Video</td>
    <td>No</td>
    <td>Yes</td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

#### description/video-file

Optional. 
No attributes. 

Some stores don't support including of YouTube videos but do supports uploaded video files. You can use this tag to link to local video files about the product. You can include several different video files.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
    <th>Number</th>
    <th>Format</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Images & Multimedia / Video(s)</td>
    <td>No</td>
    <td>No</td>
    <td>0-5</td>
    <td>MPEG-2, WMV, MOV, FLV, AVI, or H.264 MPEG-4, Minimum 720px wide (4:3 or 16:9); 1200 kbps or higher</td>
  </tr>
</table>

### content-description
Required.
No attributes.

This section describes what activities that could be considered questionable the program/game includes. The stores using this information for filtering to show the app only to people who whom it is allowed. The three main subsections describe age restrictions and existing certificates, content descriptors that are used to calculate age restrictions and other questionable application activities that should require user and/or parent understanding but that are not covered by Android permissions.  

Example:
```xml
<content-description>
  <content-rating>12</content-rating>
  <rating-certificates>
    <rating-certificate type="PEGI" certificate="whirl-pegi.pdf">7</rating-certificate>
    <rating-certificate type="ESRB" certificate="whirl-esrb.pdf">7</rating-certificate>
    <rating-certificate type="GRB" certificate="whirl-grb.pdf">all</rating-certificate>
    <rating-certificate type="CERO" certificate="whirl-cero.pdf">all</rating-certificate>
    <rating-certificate type="DEJUS" certificate="whirl-dejus.pdf" mark="dejus_mark.jpg">l</rating-certificate>
    <rating-certificate type="FSK" certificate="whirl-fsk.pdf">0</rating-certificate>
  </rating-certificates>
  <content-descriptors>
    <cartoon-violence>no</cartoon-violence>
    <realistic-violence>no</realistic-violence>
    <bad-language>no</bad-language>
    <fear>light</fear>
    <sexual-content>no</sexual-content>
    <drugs>no</drugs>
    <gambling-refference>no</gambling-refference>
    <alcohol>no</alcohol>
    <smoking>strong</smoking>
    <discrimination>no</discrimination
  </content-descriptors>
  <included-activities>
    <in-app-billing>no</in-app-billing>
    <gambling>no</gambling>
    <advertising>no</advertising>
    <user-generated-content>no</user-generated-content>
    <user-to-user-communications>no</user-to-user-communications>
    <account-creation>no</account-creation>
    <personal-information-collection>no</personal-information-collection>
  </included-activities>
</content-description>
```

#### content-description/content-rating
Required.
No attributes.

Each application must be labeled with a minimum allowed age according to [ESRB standard](http://en.wikipedia.org/wiki/Entertainment_Software_Rating_Board). Tag value must be a number of minimum age which could be `3`, `6`, `10`, `13`, `17`, or `18`. 

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Categorization / Content rating</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
</table>

There is no universal content rating system (aka parental control rating, aka minimum age). Different stores uses different systems. AppDF uses ESRB standard but more important is how this information is mapped to the systems used in the appstores. The following table is used by AppDF to convert the rating to the systems of all the main application stores.

<table>
  <tr>
    <th>ESRB</th>
    <th>Google Play</th>
    <th>Amazon AppStore</th>
  </tr>
  <tr>
    <td>3</td>
    <td>Everyone</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Low maturity</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>10</td>
    <td>Medium maturity</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>13</td>
    <td>Medium maturity</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>17</td>
    <td>High maturity</td>
    <td>n/a</td>
  </tr>
  <tr>
    <td>18</td>
    <td>High maturity</td>
    <td>n/a</td>
  </tr>
</table>

There could be exceptional products for which a generic convertion rules described in this table don't work. You can use the `<store-specific>` tag to specify a custom content rating for the stores in that case.

Here you can find more detailed information about content rating definitions used in different stores:
<table>
  <tr>
    <th>Store</th>
    <th>Link</th>
  </tr>
  <tr>
    <td>ESRB (used in AppDF)</td>
    <td>http://en.wikipedia.org/wiki/Entertainment_Software_Rating_Board</td>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>http://support.google.com/googleplay/android-developer/support/bin/answer.py?hl=en&answer=188189</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Uses several content descriptors instead of one rating value</td>
  </tr>
</table>

##### Notes:
1. Amazon hasn't one field for application rating but uses several parameters (nudity, violation, etc)
2. Samsung uses minimum age parameter along with several other attributes that define application rating according to the standard certification systems (PEGI, ESRB, etc)

#### content-description/rating-certificates/rating-certificate
Optional.
Attributes: `type`, `certificat`, `mark`. 

If your application/game has a rating certificate issued by one of the authorities you can include it using the optional tag `<rating-certificate>`. Tag value should be rating given you, usually it is a minimum age number.
 
Example:
```xml
<rating-certificates>
  <rating-certificate type="PEGI" certificate="whirl-pegi.pdf">7</rating-certificate>
  <rating-certificate type="ESRB" certificate="whirl-esrb.pdf">7</rating-certificate>
  <rating-certificate type="GRB" certificate="whirl-grb.pdf">all</rating-certificate>
  <rating-certificate type="CERO" certificate="whirl-cero.pdf">all</rating-certificate>
  <rating-certificate type="DEJUS" certificate="whirl-dejus.pdf" mark="dejus_mark.jpg">l</rating-certificate>
  <rating-certificate type="FSK" certificate="whirl-fsk.pdf">0</rating-certificate>
</rating-certificates>
```

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Required</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>type</td>
    <td>PEGI, ESRB, GRB, CERO, DEJUS or FSK</td>
    <td>required</td>
    <td>Name of the content rating certificate</td>
  </tr>
  <tr>
    <td>certificate</td>
    <td>File name from the AppDF package</td>
    <td>optional</td>
    <td>If you have a scanned certificate you can add it there</td>
  </tr>
  <tr>
    <td>mark</td>
    <td>File name from the AppDF package</td>
    <td>optional</td>
    <td>If you have a special label you can add it there</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Certificates</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

#### content-description/content-descriptors
Required.
No attributes.

Contains several subtags each describing one of the content descriptors. Each content descriptor could have either `no`, `light` or `strong` value. Most of the stores do not use this information but rather use summary information from the `<minimum-age>` tag. You can read more detailed description of these categories in the articles about the content rating systems:
[ESRB](http://en.wikipedia.org/wiki/Entertainment_Software_Rating_Board), [PEGI](http://en.wikipedia.org/wiki/Pan_European_Game_Information).

Example:
```xml
<content-descriptors>
  <cartoon-violence>no</cartoon-violence>
  <realistic-violence>no</realistic-violence>
  <bad-language>no</bad-language>
  <fear>light</fear>
  <sexual-content>no</sexual-content>
  <drugs>no</drugs>
  <gambling-refference>no</gambling-refference>
  <alcohol>no</alcohol>
  <smoking>strong</smoking>
  <discrimination>no</discrimination>
</content-descriptors>
```

<table>
  <tr>
    <th>Content descriptor</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td>cartoon-violence</td>
    <td>Violent actions involving cartoon-like situations and characters. May include violence where a character is unharmed after the action has been inflicted</td>
  </tr>
  <tr>
    <td>realistic-violence</td>
    <td>May contain scenes of people getting injured or dying, often by use of weapons. Also may contain gore and blood-letting.</td>
  </tr>
  <tr>
    <td>fear</td>
    <td>May contain scenes that are considered too disturbing or frightening to younger or more emotionally vulnerable players.</td>
  </tr>
  <tr>
    <td>sexual-content</td>
    <td>May contain references to sexual attraction or sexual intercourse. Also may contain nudity and characters dressed in suggestive clothing.</td>
  </tr>
  <tr>
    <td>drugs</td>
    <td>May contain references to illegal drugs or a fictional substance that has parallels to real-life illegal drugs (in use, possession, or sale).</td>
  </tr>
  <tr>
    <td>gambling-refference</td>
    <td>May contain elements that encourage or teach gambling.</td>
  </tr>
  <tr>
    <td>alcohol</td>
    <td>The consumption of alcoholic beverages or references to and/or images or alcoholic beverages</td>
  </tr>
  <tr>
    <td>smoking</td>
    <td>References to and/or images of tobacco products</td>
  </tr>
  <tr>
    <td>discrimination</td>
    <td>May contain cruelty or harassment based on race, ethnicity, gender, or sexual preferences.</td>
  </tr>
  <tr>
    <td>bad-language</td>
    <td>May contain profanity, sexual innuendo, threats, and all manner of slurs and epithets.</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Content Rating</td>
    <td>Yes</td>
    <td></td>
  </tr>
</table>

#### content-description/included-activities
Required.
No attributes.

Contains several subtags each describing one type of the application activities that may require user or parent understanding and permission but that is not covered by Android permission system. Each activity tag could have either `no`, `yes` value. 

Example:
```xml
<included-activities>
  <in-app-billing>no</in-app-billing>
  <gambling>no</gambling>
  <advertising>no</advertising>
  <user-generated-content>no</user-generated-content>
  <user-to-user-communications>no</user-to-user-communications>
  <account-creation>no</account-creation>
  <personal-information-collection>yes</personal-information-collection>
</included-activities>
```

<table>
  <tr>
    <th>Activity</th>
    <th>Explanation</th>
  </tr>
  <tr>
    <td>in-app-billing</td>
    <td>Either standard or custom in-app billing (aka In-App Purchases)</td>
  </tr>
  <tr>
    <td>gambling</td>
    <td>Gambling</td>
  </tr>
  <tr>
    <td>advertising</td>
    <td>Any form of advertising including banner or AirPush-like advertising</td>
  </tr>
  <tr>
    <td>user-generated-content</td>
    <td>User generated content</td>
  </tr>
  <tr>
    <td>user-to-user-communications</td>
    <td>User to user communications</td>
  </tr>
  <tr>
    <td>account-creation</td>
    <td>Account creation</td>
  </tr>
  <tr>
    <td>personal-information-collection</td>
    <td>Your application transfers to the server or collects locally on the device any personal information</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Content Rating</td>
    <td>Yes</td>
    <td></td>
  </tr>
</table>

### availability
Optional.
No attributes.

You can define country list of period of time where/when you application is distributed. By default your application is distributed in all the countries where language support allows.

Example:
```xml
<availability>
  <countries>
    <include>en</include>
    <include>ru</include>
    <exclude>de</exclude>
  <countries>

  <period>
    <since year="2012" month="12" day="23"/>
    <until year="2013" month="12" day="23"/>
  </period>
</availability>
```

#### availability/countries
Optional.
No attributed.

Use `<include>` and `<exclude>` subtags to define list of the countries where your application is distributed.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Pricing and Distribution / Distribute in These Countries</td>
    <td>No</td>
    <td>Supports only &lt;exclude&gt;. Many countries are united under "Rest of the world" block and cannot be checked/unchecked one by one</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Availability & Pricing / Where would you like this app to be available?</td>
    <td>No</td>
    <td></td>
  </tr>
</table>

#### availability/period/since
Optional.
Attributes: `year`, `month`, `day`. 

If presented this tag defines a date from which the application can be distributed. Stores that support this tag will not distribute the app before this date. 

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>year</td>
    <td>A number like 2012</td>
    <td>required</td>
    <td>Year of the date</td>
  </tr>
  <tr>
    <td>month</td>
    <td>Month number, Jan=1, Feb=2, ..., Dec=12</td>
    <td>required</td>
    <td>Month of the date</td>
  </tr>
  <tr>
    <td>day</td>
    <td>Number of the day between 1 and 31</td>
    <td>required</td>
    <td>Day of the date</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Availability & Pricing / When would you like this app to be available on Amazon?</td>
    <td>No</td>
  </tr>
</table>

#### availability/period/until
Optional.
Optional.
Attributes: `year`, `month`, `day`. 

If presented this tag defines a final date of application distribution. Stores that support this tag will not distribute the app after this date. 

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>year</td>
    <td>A number like 2012</td>
    <td>required</td>
    <td>Year of the date</td>
  </tr>
  <tr>
    <td>month</td>
    <td>Month number, Jan=1, Feb=2, ..., Dec=12</td>
    <td>required</td>
    <td>Month of the date</td>
  </tr>
  <tr>
    <td>day</td>
    <td>Number of the day between 1 and 31</td>
    <td>required</td>
    <td>Day of the date</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Availability & Pricing / When would you like this app to be discontinued for sale?</td>
    <td>No</td>
  </tr>
</table>

### price
Required.
Attributes: `free`. 

This section describes whether the application is free or paid and if paid what is its price. It has also an option for free apps to mark them as trial version of another app.

Example:
```xml
<price free="yes">
  <base-price currency="USD">4.95</base-price>
  <local-price country="de" currency="EUR">3.95</local-price>
  <local-price country="fr" currency="EUR">3.95</local-price>
  <local-price country="ru" currency="RUB">99</local-price>
  <trial-version full-version="com.yandex.shellfullversion"/>
</price>
```

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>free</td>
    <td>yes or no</td>
    <td>yes</td>
    <td>&lt;base-price&gt; and &lt;local-price&gt; subtags are applicable for paid apps, &lt;trial-version&gt; subtag is applicable for free apps</td>
  </tr>
</table>

#### price/base-price
Required for paid apps.
Attributes: `currency`. 

Application price. Tag value should be a dot-separated number. This price is used to automatically calculate the prices in other currencies unless you manually specify such prices using `<local-price>` tags.

This tag is ignored for free apps.

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>currency</td>
    <td>?todo</td>
    <td>USD</td>
    <td>?todo</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Currency</th>
    <th>Including sales tax</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Pricing and Distribution / Default Price</td>
    <td>USD</td>
    <td>Yes</td>
    <td>Up to a cent precision</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Availability & Pricing / Are you charging for this app?</td>
    <td>USD, EUR, GBR, JPY</td>
    <td>Yes</td>
    <td>Up to a cent precision</td>
  </tr>
</table>

#### price/local-price
Optional.
Attributes: `country`, `currency`. 

The stores will use your default price defined in the `<base-price>` tag to automatically generate prices for other currencies and other countries. Nevertheless you can use `<local-price>` tags to manually define price for some countries. Tag value should be a dot-separated number.

This tag is ignored for free apps.

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>country</td>
    <td>two letter ISO 3166-1 country code</td>
    <td>required</td>
    <td></td>
  </tr>
  <tr>
    <td>currency</td>
    <td>Three capital letter ISO 4217 currency code</td>
    <td>required</td>
    <td></td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Including sales tax</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Pricing and Distribution / Country List / Price</td>
    <td>Yes</td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Availability & Pricing / Calculated prices</td>
    <td>Yes</td>
    <td>Only US, UK, DE, FR, ES, IT, JP are supported</td>
  </tr>
</table>

#### price/trial-version
Optional.
Attributes: `full-version`. 

If presented this tag indicates that this free app is a trial/demo version of another application. `full-version` attribute defines package name of the corresponding full version application.

This tag is ignored for paid apps.

<table>
  <tr>
    <th>Attribute</th>
    <th>Possible values</th>
    <th>Default</th>
    <th>How it works</th>
  </tr>
  <tr>
    <td>full-version</td>
    <td>package name (Android notation)</td>
    <td>required</td>
    <td></td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
  </tr>
</table>

### apk-files
Required.
No attributes.

In this section you list your APK. Each application could consist of several APK files. Google Play (and may be other stores in future) also supports APK extension files. The subtags should be either `<apk-file>` for normal APK files or `<apk-file-with-extnsion>` for APK files with extension(s). 

Please note that today the only application store supporting APK file with extensions is Google Play. So by using `<apk-file-with-extnsion>` tag you limit your application to Google Play only today.

Example:
```xml
<apk-files>
  <apk-file>yandexshell2.apk</apk-file>
  <apk-file>yandexshell3.apk</apk-file>
  <apk-file-with-extnsion>
    <apk-file>yandexshell4.apk</apk-file>
    <extension>extensionfile.zip</extension>
  </apk-file-with-extnsion>
</apk-files>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Maximum APK file size</th>
    <th>Multiple APK file support</th>
    <th>Extension file support</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>APK / Upload new APK</td>
    <td>50M</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Binary File(s) / Binary file</td>
    <td>Unlimited</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
</table>

### requirements
Optional.
No attributes.

You can use this section if you application has some special requirements apart of requirements described in the APK file.

Example:
```xml
<requirements>
  <features>
    <root>no</root>
    <gms>no</gms>
  </features>

  <supported-languages>
    <language>en</language>
    <language>ru</language>
    <language>de</language>
    <language>fr</language>
    <language>it</language>
  </supported-languages>

  <supported-devices>
    <exclude>kyleopen</exclude>
    <exclude>SHW-M130K</exclude>
  </supported-devices>

  <supported-resolutions>
    <exclude>480x856</exclude>
    <include>240x400</include>
  </supported-resolutions>
</requirements>
```

#### requirements/features

#### requirements/supported-languages
Optional.
No attributes.

You man manually define the list of supported languages. Add `<language>` subtag with two letter ISO 639-1 language codes for each language the application supports.

Example:
```xml
<supported-languages>
  <language>en</language>
  <language>ru</language>
  <language>de</language>
  <language>fr</language>
  <language>it</language>
</supported-languages>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Binary File(s) / Language Support</td>
    <td></td>
  </tr>
</table>



#### requirements/supported-devices
Optional.
No attributes.

You man manually exclude some devices from the supported device list. Add `<exclude>` tag with device model name (aka [name of the industrial design](http://developer.android.com/reference/android/os/Build.html#DEVICE)) for each device you want to exclude from the compatibility list.

Example:
```xml
<supported-devices>
  <exclude>kyleopen</exclude>
  <exclude>SHW-M130K</exclude>
</supported-devices>
```

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>APK / Device Compatibility</td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>No</td>
    <td></td>
    <td></td>
  </tr>
</table>


#### requirements/supported-resolutions

### store-specific
Optional.
No attributes.

All store specific information is collected in this section. 

Example:
```xml
<store-specific>
  <amazon>
    <form-factor>all</form-factor>
    <free-app-of-the-day-eligibility>yes</free-app-of-the-day-eligibility>
    <apply-amazon-drm>yes</apply-amazon-drm>
    <kindle-support>
      <kindle-fire-first-generation>yes</kindle-fire-first-generation>
      <kindle-fire>yes</kindle-fire>
      <kindle-fire-hd>yes</kindle-fire-hd>
      <kindle-fire-hd-8-9>yes</kindle-fire-hd-8-9>
    </kindle-support>
    <binary-alias>Version 1</binary-alias>
  </amazon>
  <samsung>
    <form-factor>phone,tablet</form-factor>
    <contains-zirconia-protection>yes</contains-zirconia-protection>
    <s-pen>yes</s-pen> 
    <tags>
      <tag>Education / Video</tag>
      <tag>Music / Album</tag>
    </tags>
  </samsung>
  <slideme>
    <license-type>apache2</license-type>
  </slideme>
</store-specific>
```

Top level subtags correspond to the application AppDF ids from the following table:

<table>
  <tr>
    <th>Application Store</th>
    <th>AppDF store id</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>google</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>amazon</td>
  </tr>
  <tr>
    <td>Opera Mobile Store</td>
    <td>opera</td>
  </tr>
  <tr>
    <td>Yandex.Store</td>
    <td>yandex</td>
  </tr>
  <tr>
    <td>SlideME</td>
    <td>slideme</td>
  </tr>
  <tr>
    <td>Samsung Apps</td>
    <td>samsung</td>
  </tr>
  <tr>
    <td>NOOK apps</td>
    <td>nook</td>
  </tr>
</table>

Each store subtag can replace any of the parameters from the entire description.xml by including a replacement for the corresponding tag starting from the `<application>` tag. For example if we want to use another large promotion picture for Amazon AppStore we can include the following code:
```xml
<store-specific>
  <amazon>
    <application>
      <description language="en">
        <images>
          <large-promo>promo_amazon.png</large-promo>
        </images> 
    </application>
  </amazon>
</store-specific>
```

There are also some optional and required store specific parameters you can/must use if you want that your AppDF file is supported by the corresponding store. 

#### store-specific/amazon
Optional.
No attributes.

Example:
```xml
<amazon>
  <form-factor>all</form-factor>
  <free-app-of-the-day-eligibility>yes</free-app-of-the-day-eligibility>
  <apply-amazon-drm>yes</apply-amazon-drm>
  <kindle-support>
    <kindle-fire-first-generation>yes</kindle-fire-first-generation>
    <kindle-fire>yes</kindle-fire>
    <kindle-fire-hd>yes</kindle-fire-hd>
    <kindle-fire-hd-8-9>yes</kindle-fire-hd-8-9>
  </kindle-support>
  <binary-alias>Version 1</binary-alias>
</amazon>
```

<table>
  <tr>
    <th>Tag</th>
    <th>Required</th>
    <th>Amazon name</th>
    <th>Possible values</th>
    <th>Comments</th>
  </tr>
  <tr>
    <td>form-factory</td>
    <td>Yes</td>
    <td>General Information / Form Factor</td>
    <td>phone, tablet, all</td>
    <td></td>
  </tr>
  <tr>
    <td>free-app-of-the-day-eligibility</td>
    <td>No</td>
    <td>Availability & Pricing / Free App of the Day (FAD) eligibility</td>
    <td>yes, no</td>
    <td>If your app is being considered, we will contact you with more detail about the program and what to expect as your app goes through the approval process.</td>
  </tr>
  <tr>
    <td>apply-amazon-drm</td>
    <td>Yes</td>
    <td>Binary File(s) / Apply Amazon DRM?</td>
    <td>yes, no</td>
    <td>Protect your application from unauthorized use. Without DRM, your app can be used without restrictions by any user.</td>
  </tr>
  <tr>
    <td>binary-alias</td>
    <td>Yes</td>
    <td>Binary File(s) / Binary1</td>
    <td>Alphanumeric characters, dots (.), and underscores (_) only.</td>
    <td>This name is used to distinguish between multiple binary files</td>
  </tr>
  <tr>
    <td>kindle-support/kindle-fire-first-generation</td>
    <td>Yes</td>
    <td>Binary File(s) / Device Support</td>
    <td>yes, no</td>
    <td>Kindle Fire (1st Generation) support</td>
  </tr>
  <tr>
    <td>kindle-support/kindle-fire</td>
    <td>Yes</td>
    <td>Binary File(s) / Device Support</td>
    <td>yes, no</td>
    <td>Kindle Fire support</td>
  </tr>
  <tr>
    <td>kindle-support/kindle-fire-hd</td>
    <td>Yes</td>
    <td>Binary File(s) / Device Support</td>
    <td>yes, no</td>
    <td>Kindle Fire HD support</td>
  </tr>
  <tr>
    <td>kindle-support/kindle-fire-hd-8-9</td>
    <td>Yes</td>
    <td>Binary File(s) / Device Support</td>
    <td>yes, no</td>
    <td>Kindle Fire HD 8.9 support</td>
  </tr>
</table>


### testing-instructions
Optional.
No attributes.

Please detail any special requirements to test your app.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Maximum size</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>No</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>Binary File(s) / Testing instructions</td>
    <td>No</td>
    <td>4000</td>
  </tr>
</table>

### consent
Required.
No attributes.

You must consent with a number of statements in order your application is published. This section includes the list of such agreements. Without this section some stores will not accept your application.  Each subtag corresponds to one of the statements you consent with. Subtag values must always be `yes` if you want your application is accepted by the corresponding stores.

Example:
```xml
<consent>
  <google-android-content-guidelines>yes</google-android-content-guidelines>
  <us-export-laws>yes</us-export-laws>
</consent>
```

<table>
  <tr>
    <th>Subtag</th>
    <th>Statement</th>
    <th>Detailed information</th>
  </tr>
  <tr>
    <td>&lt;google-android-content-guidelines&gt;</td>
    <td>This application meets Android Content Guidelines</td>
    <td>http://play.google.com/about/developer-content-policy.html</td>
  </tr>
  <tr>
    <td>&lt;us-export-laws&gt;</td>
    <td>I acknowledge that my software application may be subject to United States export laws, regardless of my location or nationality. I agree that I have complied with all such laws, including any requirements for software with encryption functions. I hereby certify that my application is authorized for export from the United States under these laws. </td>
    <td>https://support.google.com/googleplay/android-developer/support/bin/answer.py?hl=en&answer=113770</td>
  </tr>
</table>

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Pricing and Distribution / Consent</td>
    <td>&lt;google-android-content-guidelines&gt;, &lt;us-export-laws&gt;</td>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Binary File(s) / Export Compliance</td>
    <td>&lt;us-export-laws&gt;</td>
  </tr>
</table>

### customer-support
Required.
No attributes.

Example:
```xml
<customer-support>
  <phone>+1 (555) 1234-56-78</phone>
  <email>support@yandex-team.ru</email>
  <website>http://www.yandex.ru/support</website>
</customer-support>
```

#### customer-support/phone
Required.
No attributes.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Contact Details / Phone</td>
    <td>No</td>
    <td>No</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Customer support phone</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
</table>

#### customer-support/email
Required.
No attributes.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Contact Details / Email</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Customer support email address</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
</table>

#### customer-support/website
Required.
No attributes.

<table>
  <tr>
    <th>Store support</th>
    <th>Supported</th>
    <th>Name</th>
    <th>Required</th>
    <th>Localizable</th>
  </tr>
  <tr>
    <td>Google Play</td>
    <td>Yes</td>
    <td>Store Listing / Contact Details / Website</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
  <tr>
    <td>Amazon AppStore</td>
    <td>Yes</td>
    <td>General Information / Customer support website</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
</table>

Application Store Support
-------------
AppDF provides universal category list that could be matched to any appstore category list. When we chose categories for the AppDF we tried to create the most detailed list to archive unambiguous mapping for any appstore.

<table>
<tr>
<th>Feature</th>
  <th>Google Play</th>
  <th>Amazon AppStore</th>
  <th>Opera Mobile Store</th>
  <th>Yandex.Store</th>
  <th>SlideME</th>
  <th>Samsung Apps</th>
  <th>NOOK- apps</th>
</tr>
<tr>
<td>Registration URL
</td>
  <td><a href="https://play.google.com/apps/publish/">Link</a></td>
  <td><a href="https://developer.amazon.com/welcome.html">Link</a></td>
  <td><a href="http://apps.opera.com/developers.php">Link</a></td>
  <td><a href="https://developer.store.yandex.com/">Link</a></td>
  <td><a href="http://slideme.org/developers">Link</a></td>
  <td><a href="http://seller.samsungapps.com/">Link</a></td>
  <td><a href="https://nookdeveloper.barnesandnoble.com/">Link</a></td>
</tr>
<tr>
<td>Distribution agreement URL
</td>
  <td><a href="http://play.google.com/intl/ALL_en/about/developer-distribution-agreement.html">Link</a></td>
  <td><a href="https://developer.amazon.com/help/da.html">Link</a></td>
  <td><a href="http://apps.opera.com/docs/DistributionAgreementHandster_standard.pdf">Link</a></td>
  <td><a href="http://legal.yandex.com/store_developer_agreement/">Link</a></td>
  <td><a href="http://slideme.org/developer-conditions">Link</a></td>
  <td><a href="http://seller.samsungapps.com/help/termsAndConditions.as">Link</a></td>
  <td>?</td>
</tr>
<tr>
<td>AppDF ID</td>
  <td>google</td>
  <td>amazon</td>
  <td>opera</td>
  <td>yandex</td>
  <td>slideme</td>
  <td>samsung</td>
  <td>nook</td>
</tr>
<tr>
<td>Registration fee</td>
  <td>$25</td>
  <td>free</td>
  <td>free</td>
  <td>free</td>
  <td>free</td>
  <td>free</td>
  <td>?</td>
</tr>
<tr>
<td>Content premoderation</td>
  <td>No</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>No</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>?</td>
</tr>
<tr>
<td>Client Application</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>No</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>Yes</td>
</tr>
<tr>
<td>In-App Purchase Support</td>
  <td>Yes</td>
  <td>Yes</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>Yes</td>
  <td>?</td>
</tr>
<tr>
<td>License verification support</td>
  <td>Yes</td>
  <td>?</td>
  <td>RPN or serial numbers</td>
  <td>No</td>
  <td>Yes</td>
  <td>Samsung DRM</td>
  <td>?</td>
</tr>
<tr>
<td>Title field name</td>
  <td><strong>Title</strong></td>
  <td><strong>App title</strong></td>
  <td><strong>Title</strong></td>
  <td><strong>Title</strong></td>
  <td>?</td>
  <td><strong>Application Title</strong></td>
  <td>?</td>
</tr>
<tr>
<td>Title maximum length</td>
  <td>30</td>
  <td>250</td>
  <td>unlimited</td>
  <td>unlimited</td>
  <td>?</td>
  <td>unlimited</td>
  <td>?</td>
</tr>
<tr>
<td>Short description field name</td>
  <td>Promo text</td>
  <td><strong>Short description</strong></td>
  <td><strong>Short Description</strong></td>
  <td>Promo text</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
</tr>
<tr>
<td>Short description maximum length</td>
  <td>80</td>
  <td>1200</td>
  <td>unlimited</td>
  <td>unlimited</td>
  <td>500</td>
  <td><del>unsupported</del></td>
  <td>?</td>
</tr>
<tr>
<td>Full description field name</td>
  <td><strong>Description</strong></td>
  <td><strong>Long description</strong></td>
  <td><strong>Full Description</strong></td>
  <td>Description</td>
  <td>?</td>
  <td><strong>Description</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Full description maximum length</td>
  <td>4000</td>
  <td>4000</td>
  <td>unlimited</td>
  <td>unlimited</td>
  <td>unlimited</td>
  <td>4000</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Full description tags</td>
  <td>?</td>
  <td>Plain text</td>
  <td>?Some HTML subset</td>
  <td>Plain text</td>
  <td>a, em, strong, cite, code, ul, ol, li, h4, h5, dl, dt, dd, img</td>
  <td>Plain text</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Recent changes field name</td>
  <td>Recent changes</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>What’s new</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Keywords field name</td>
  <td>?</td>
  <td>Keywords</td>
  <td>Keywords</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>Other Tags</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Feature list field name</td>
  <td><del>unsupported</del></td>
  <td>
<strong>Product feature bullets</strong>, 3-5 lines</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Maximum APK file size</td>
  <td>50M</td>
  <td>Unlimited</td>
  <td>?</td>
  <td>Unlimited</td>
  <td>66M</td>
  <td>Unlimited</td>
	</tr>
<tr>
<td>
APK Expansion Files support</td>
  <td>Yes</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Screenshots field name</td>
  <td><strong>Screenshots</strong></td>
  <td><strong>Screenshots</strong></td>
  <td>
<strong>Main image</strong>, Images</td>
  <td><strong>Screenshots</strong></td>
  <td>?</td>
  <td><strong>Screenshots</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Screenshot image</td>
  <td>320×480, 480×800, 480×854, 1280×720, 1280×800</td>
  <td>800×480, 1024×600, 1280×720,<br>
1280×800, 1920×1200 (portrait or landscape)</td>
  <td>?</td>
  <td>?</td>
  <td>240×180 – 640×480, &lt;500K</td>
  <td>480×800 or 800×480</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Number of screenshots</td>
  <td>2-8</td>
  <td>3-10</td>
  <td>1-3</td>
  <td>2+</td>
  <td>0-3</td>
  <td>4</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Screenshot formats</td>
  <td>
JPG, PNG, no alpha</td>
  <td>
PNG, JPG
</td>
  <td>?</td>
  <td>?</td>
  <td>
JPG, PNG, GIF
</td>
  <td>
JPG, GIF, PNG
</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Application icon field name</td>
  <td><strong>High-res icon</strong></td>
  <td><strong>Large icon</strong></td>
  <td><strong>Thumbnail</strong></td>
  <td><strong>High resolution application icon</strong></td>
  <td>?</td>
  <td><strong>Icon Image</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Application icon resolution</td>
  <td>512×512</td>
  <td>512×512 + 114×114</td>
  <td>preferably 512×512</td>
  <td>512×512</td>
  <td>150×150 – 500×500</td>
  <td>135×135</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Application icon formats</td>
  <td>
PNG with alpha</td>
  <td>
PNG with alpha</td>
  <td>?</td>
  <td>?</td>
  <td>
JPG, PNG, GIF
</td>
  <td>
JPG, GIF
</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Promotion image field name</td>
  <td>Feature Graphic</td>
  <td>Promotional image</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Promotion image resolution</td>
  <td>1024×500</td>
  <td>1024 × 500</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>1024×500, &lt;1M</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Small promotion field name</td>
  <td>Promo Graphic</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Small promotion image resolution</td>
  <td>180×120</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>180×120, &lt;256K</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Promotion image formats</td>
  <td>
JPG, PNG no alpha</td>
  <td>
PNG, JPG
</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>1024×500, &lt;1M</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>YouTube video field name</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>YouTube URL
</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Root access option</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>No</td>
  <td>Yes</td>
	</tr>
<tr>
<td>Custom resolution setting</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>Yes</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Manual language list editinh</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>?</td>
  <td>Yes</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Application type field name</td>
  <td><strong>Application type</strong></td>
  <td>?</td>
  <td>?</td>
  <td><strong>Categories</strong></td>
  <td>?</td>
  <td><strong>Category / Primary</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Category field name</td>
  <td><strong>Category</strong></td>
  <td><strong>Category</strong></td>
  <td><strong>Category</strong></td>
  <td><strong>Categories</strong></td>
  <td>?</td>
  <td><strong>Category / Primary</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Subcategory field name</td>
  <td><del>Not used</del></td>
  <td><strong>Category</strong></td>
  <td><del>Not used</del></td>
  <td><del>not used</del></td>
  <td>?</td>
  <td>Category / Secondary</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Minimum age field name</td>
  <td><strong>Content rating</strong></td>
  <td>
<del>unsupported</del>, list of options instead</td>
  <td>?</td>
  <td><strong>Age rating</strong></td>
  <td>?</td>
  <td><strong>Age Restriction</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Customer support / Email</td>
  <td><strong>Contact details / Email</strong></td>
  <td><strong>Customer support email address</strong></td>
  <td>Contact Email</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><strong>Support E-Mail</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Customer support / Website</td>
  <td><strong>Contact details / Website</strong></td>
  <td><strong>Customer support website</strong></td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>Support URL
</td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Customer support / Phone</td>
  <td>Contact details / Phone</td>
  <td><strong>Customer support phone</strong></td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>EULA</td>
  <td><del>unsupported</del></td>
  <td><del>unsupported</del></td>
  <td>Text or link</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Privacy policy</td>
  <td>?</td>
  <td>
URL, requires if information collected</td>
  <td>Text or link</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>“available-since” Support</td>
  <td>?</td>
  <td>Yes</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>Yes</td>
	</tr>
<tr>
<td>“available-until” Support</td>
  <td>?</td>
  <td>Yes</td>
  <td>?</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td>Yes</td>
	</tr>
<tr>
<td>Testing instructions</td>
  <td>No</td>
  <td>Yes</td>
  <td>No</td>
  <td><del>unsupported</del></td>
  <td>?</td>
  <td><strong>Comments to Certification Team</strong></td>
  <td>?</td>
  <td>?</td>
	</tr>
<tr>
<td>Consent</td>
  <td>Android Content Guidelines, US Export Laws</td>
  <td>Export Compliance</td>
  <td>?</td>
  <td>no</td>
  <td>?</td>
  <td>no</td>
  <td>?</td>
  <td>?</td>
	</tr>
</table>

### Application Categories

Category List
-------------
AppDF provides universal category list that could be matched to any appstore category list. When we chose categories for the AppDF we tried to create the most detailed list to archive unambiguous mapping for any appstore.

### Application Categories

<table>
<tr>
  <th>Category</th>
  <th>Google Play</th>
  <th>Amazon AppStore</th>
  <th>Opera Store</th>
  <th>Yandex.Store</th>
  <th>Samsung Apps</th>
  <th>SlideMe</th>
</tr>
<tr>
<td>Comics</td>
  <td>Comics</td>
  <td>Books &amp; Comic / Comic Strips</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications / Comics</td>
</tr>
<tr>
<td>Books</td>
  <td>Books &amp; Reference</td>
  <td>Books &amp; Comic / Other</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications / E-books</td>
</tr>
<tr>
<td>Publications</td>
  <td>Books &amp; Reference</td>
  <td>Books &amp; Comic / Other</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications</td>
</tr>
<tr>
<td>Books &amp; Readers</td>
  <td>Books &amp; Reference</td>
  <td>Books &amp; Comic / Books &amp; Readers</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications / E-book readers</td>
</tr>
<tr>
<td>Children’s Books</td>
  <td>Books &amp; Reference</td>
  <td>Books &amp; Comic / Children’s Books</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications</td>
</tr>
<tr>
<td>Graphic Novels</td>
  <td>Books &amp; Reference</td>
  <td>Books &amp; Comic / Graphic Novels</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications</td>
</tr>
<tr>
<td>Reference</td>
  <td>Books &amp; Reference</td>
  <td>Reference</td>
  <td>eBooks</td>
  <td>eBooks</td>
  <td>Education/E-Book</td>
  <td>Publications</td>
</tr>
<tr>
<td>City Info</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Other</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>Country Guides</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Other</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / Country Guides</td>
</tr>
<tr>
<td>City Info / Boston</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Boston</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Chicago</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Chicago</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Dallas</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Dallas</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Los Angeles</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Los Angeles</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Miami</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Miami</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / New York</td>
  <td>Books &amp; Reference</td>
  <td>City Info / New York</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Philadelphia</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Philadelphia</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Phoenix</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Phoenix</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / San Francisco</td>
  <td>Books &amp; Reference</td>
  <td>City Info / San Francisco</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>City Info / Seattle</td>
  <td>Books &amp; Reference</td>
  <td>City Info / Seattle</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Reference</td>
  <td>Travel &amp; Locality / City Guides</td>
</tr>
<tr>
<td>Weather</td>
  <td>Weather</td>
  <td>News &amp; Weather / Weather</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Weather</td>
  <td>News &amp; Weather / Weather</td>
</tr>
<tr>
<td>Travel / Transportation</td>
  <td>Transportation</td>
  <td>Travel / Transportation</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality / Other</td>
</tr>
<tr>
<td>Travel</td>
  <td>Travel &amp; Local</td>
  <td>Travel / Other</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality</td>
</tr>
<tr>
<td>Travel / Auto Rental</td>
  <td>Travel &amp; Local</td>
  <td>Travel / Auto Rental</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality / Other</td>
</tr>
<tr>
<td>Travel / Flight</td>
  <td>Travel &amp; Local</td>
  <td>Travel / Flight</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality / Other</td>
</tr>
<tr>
<td>Travel / Hotel</td>
  <td>Travel &amp; Local</td>
  <td>Travel / Hotel</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality / Other</td>
</tr>
<tr>
<td>Travel / Trip Planner</td>
  <td>Travel &amp; Local</td>
  <td>Travel / Trip Planner</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Travel</td>
  <td>Travel &amp; Locality / Other</td>
</tr>
<tr>
<td>Navigation</td>
  <td>Travel &amp; Local</td>
  <td>Navigation</td>
  <td>Travel &amp; Maps</td>
  <td>Travel &amp; Maps</td>
  <td>Navigation</td>
  <td>Travel &amp; Locality / Navigation</td>
</tr>
<tr>
<td>Religion</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion</td>
</tr>
<tr>
<td>Religion / Buddhism</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Buddhism</td>
</tr>
<tr>
<td>Religion / Chinese folk</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Chinese folk</td>
</tr>
<tr>
<td>Religion / Christianity</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Christianity</td>
</tr>
<tr>
<td>Religion / Hinduism</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Hinduism</td>
</tr>
<tr>
<td>Religion / Islam</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Islam</td>
</tr>
<tr>
<td>Religion / Other</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Religion / Other</td>
</tr>
<tr>
<td>Lifestyle</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle</td>
</tr>
<tr>
<td>Home &amp; Hobby</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Home &amp; Hobby</td>
</tr>
<tr>
<td>Home &amp; Hobby / Other</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Home &amp; Hobby / Other</td>
</tr>
<tr>
<td>Lifestyle / Advice</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Advice</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Astrology</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Astrology</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Celebrity</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrity</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrities</td>
</tr>
<tr>
<td>Lifestyle / Culture</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrity</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Culture</td>
</tr>
<tr>
<td>Lifestyle / Design</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrity</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Design</td>
</tr>
<tr>
<td>Lifestyle / Fashion</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrity</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Fashion</td>
</tr>
<tr>
<td>Lifestyle / Living</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Celebrity</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Living</td>
</tr>
<tr>
<td>Lifestyle / Hair &amp; Beauty</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Hair &amp; Beauty</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Home &amp; Garden</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Home &amp; Garden</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Parenting</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Parenting</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Quizzes &amp; Games</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Quizzes &amp; Games</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Relationships</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Relationships</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Lifestyle / Self Improvement</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Self Improvement</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Lifestyle</td>
  <td>Lifestyle / Other</td>
</tr>
<tr>
<td>Magazines</td>
  <td>News &amp; Magazines</td>
  <td>Magazines</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>Publications / Magazines</td>
</tr>
<tr>
<td>Newspapers</td>
  <td>News &amp; Magazines</td>
  <td>Newspapers</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>Publications</td>
</tr>
<tr>
<td>News</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Regional News</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / Regional News</td>
</tr>
<tr>
<td>News / Other</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / Other</td>
</tr>
<tr>
<td>News &amp; Weather</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather</td>
</tr>
<tr>
<td>News / Business</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Business</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Entertainment</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Health</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Health</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Politics</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Politics</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Science &amp; Tech</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Science &amp; Tech</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / Sports</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / Sports</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / US</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / US</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>News / World</td>
  <td>News &amp; Magazines</td>
  <td>News &amp; Weather / World</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>News/Magazine</td>
  <td>News &amp; Weather / News</td>
</tr>
<tr>
<td>Shopping</td>
  <td>Shopping</td>
  <td>Shopping</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Home &amp; Hobby / Shopping</td>
</tr>
<tr>
<td>Sports</td>
  <td>Sports</td>
  <td>Sports / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports</td>
</tr>
<tr>
<td>Sports / Athletic</td>
  <td>Sports</td>
  <td>Sports / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Athletic</td>
</tr>
<tr>
<td>Sports / Disabled</td>
  <td>Sports</td>
  <td>Sports / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Disabled</td>
</tr>
<tr>
<td>Sports / Extreme</td>
  <td>Sports</td>
  <td>Sports / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Extreme</td>
</tr>
<tr>
<td>Sports / Motor</td>
  <td>Sports</td>
  <td>Sports / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Motor</td>
</tr>
<tr>
<td>Sports / Baseball</td>
  <td>Sports</td>
  <td>Sports / Baseball</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Basketball</td>
  <td>Sports</td>
  <td>Sports / Basketball</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Boxing</td>
  <td>Sports</td>
  <td>Sports / Boxing</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Football</td>
  <td>Sports</td>
  <td>Sports / Football</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Golf</td>
  <td>Sports</td>
  <td>Sports / Golf</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Hockey</td>
  <td>Sports</td>
  <td>Sports / Hockey</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / NCAA
</td>
  <td>Sports</td>
  <td>Sports / NCAA
</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Soccer</td>
  <td>Sports</td>
  <td>Sports / Soccer</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / Tennis</td>
  <td>Sports</td>
  <td>Sports / Tennis</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Sports / UFC
</td>
  <td>Sports</td>
  <td>Sports / UFC
</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Sports</td>
  <td>Sports / Other</td>
</tr>
<tr>
<td>Novelty</td>
  <td>Entertainment</td>
  <td>Novelty</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
</tr>
<tr>
<td>Podcasts</td>
  <td>Entertainment</td>
  <td>Podcasts</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
</tr>
<tr>
<td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
</tr>
<tr>
<td>Entertainment / Comedy</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment / Comedy</td>
</tr>
<tr>
<td>Entertainment / Music</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment / Music</td>
</tr>
<tr>
<td>Entertainment / Sports</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment / Sports</td>
</tr>
<tr>
<td>Entertainment / Theatre</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment / Theatre</td>
</tr>
<tr>
<td>Entertainment / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment / Other</td>
</tr>
<tr>
<td>Video</td>
  <td>Media &amp; Video</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Music/Video</td>
  <td>Entertainment / Film</td>
</tr>
<tr>
<td>Kids</td>
  <td>Education</td>
  <td>Kids / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / All</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Alphabet</td>
  <td>Education</td>
  <td>Kids / Alphabet</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Animals</td>
  <td>Education</td>
  <td>Kids / Animals</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / History</td>
  <td>Education</td>
  <td>Kids / History</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Language</td>
  <td>Education</td>
  <td>Kids / Language</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Math</td>
  <td>Education</td>
  <td>Kids / Math</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Popular Characters</td>
  <td>Education</td>
  <td>Kids / Popular Characters</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainmenttd>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Reading</td>
  <td>Education</td>
  <td>Kids / Reading</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Science</td>
  <td>Education</td>
  <td>Kids / Science</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Kids / Writing</td>
  <td>Education</td>
  <td>Kids / Writing</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Kids / Edutainment</td>
  <td>Education / Early Childhood</td>
</tr>
<tr>
<td>Education</td>
  <td>Education</td>
  <td>Education / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education</td>
</tr>
<tr>
<td>Education / Higher</td>
  <td>Education</td>
  <td>Education / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Higher</td>
</tr>
<tr>
<td>Education / Primary</td>
  <td>Education</td>
  <td>Education / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Primary</td>
</tr>
<tr>
<td>Education / Secondary</td>
  <td>Education</td>
  <td>Education / Other</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Secondary</td>
</tr>
<tr>
<td>Education / History</td>
  <td>Education</td>
  <td>Education / History</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Math</td>
  <td>Education</td>
  <td>Education / Math</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Reading</td>
  <td>Education</td>
  <td>Education / Reading</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Science</td>
  <td>Education</td>
  <td>Education / Science</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Test Guides</td>
  <td>Education</td>
  <td>Education / Test Guides</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Writing</td>
  <td>Education</td>
  <td>Education / Writing</td>
  <td>Entertainment</td>
  <td>Entertainment</td>
  <td>Education/E-Book</td>
  <td>Education / Other</td>
</tr>
<tr>
<td>Education / Language</td>
  <td>Education</td>
  <td>Education / Language</td>
  <td>Languages &amp; Translators</td>
  <td>Languages &amp; Translators</td>
  <td>Education/E-Book</td>
  <td>Languages</td>
</tr>
<tr>
<td>Education / Dictionaries</td>
  <td>Education</td>
  <td>Education / Language</td>
  <td>Languages &amp; Translators</td>
  <td>Languages &amp; Translators</td>
  <td>Education/E-Book</td>
  <td>Languages / Dictionaries</td>
</tr>
<tr>
<td>Education / Language learning</td>
  <td>Education</td>
  <td>Education / Language</td>
  <td>Languages &amp; Translators</td>
  <td>Languages &amp; Translators</td>
  <td>Education/E-Book</td>
  <td>Languages / Language learning</td>
</tr>
<tr>
<td>Web Browsers</td>
  <td>Communication</td>
  <td>Web Browsers</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Tools &amp; Utilities / Browsers</td>
</tr>
<tr>
<td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication</td>
</tr>
<tr>
<td>Communication / E-mail</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication / E-mail</td>
</tr>
<tr>
<td>Communication / Instant Messaging</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication / Instant Messaging</td>
</tr>
<tr>
<td>Communication / SMS
</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication / SMS
</td>
</tr>
<tr>
<td>Communication / Other</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication / Other</td>
</tr>
<tr>
<td>Social</td>
  <td>Social</td>
  <td>Social Networking</td>
  <td>Communication</td>
  <td>Communication</td>
  <td>Social Networking</td>
  <td>Communication / Social Networking</td>
</tr>
<tr>
<td>Real Estate</td>
  <td>Business</td>
  <td>Real Estate</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Business</td>
  <td>Finance / Other</td>
</tr>
<tr>
<td>Business</td>
  <td>Business</td>
  <td>Finance / Other</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; FinanceBusiness</td>
  <td>Business</td>
  <td>Finance / Other</td>
</tr>
<tr>
<td>Finance</td>
  <td>Finance</td>
  <td>Finance / Other</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance</td>
</tr>
<tr>
<td>Finance / Corporate</td>
  <td>Finance</td>
  <td>Finance / Other</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance / Corporate</td>
</tr>
<tr>
<td>Finance / Other</td>
  <td>Finance</td>
  <td>Finance / Other</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance / Other</td>
</tr>
<tr>
<td>Finance / Accounting</td>
  <td>Finance</td>
  <td>Finance / Accounting</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance</td>
</tr>
<tr>
<td>Finance / Banking</td>
  <td>Finance</td>
  <td>Finance / Banking</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance</td>
</tr>
<tr>
<td>Finance / Investing</td>
  <td>Finance</td>
  <td>Finance / Investing</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance</td>
</tr>
<tr>
<td>Finance / Money &amp; Currency</td>
  <td>Finance</td>
  <td>Finance / Money &amp; Currency</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance</td>
</tr>
<tr>
<td>Personal Finance</td>
  <td>Finance</td>
  <td>Finance / Personal Finance</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Finance / Personal</td>
</tr>
<tr>
<td>Home &amp; Hobby / Budgeting</td>
  <td>Finance</td>
  <td>Finance / Personal Finance</td>
  <td>Business &amp; Finance</td>
  <td>Business &amp; Finance</td>
  <td>Finance</td>
  <td>Home &amp; Hobby / Budgeting</td>
</tr>
<tr>
<td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Other</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness</td>
</tr>
<tr>
<td>Diet &amp; Weight Loss</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Diet &amp; Weight Loss</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Calorie calculators</td>
</tr>
<tr>
<td>Health / Exercise</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Exercise &amp; Fitness</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Fitness</td>
</tr>
<tr>
<td>Health / Medical</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Medical</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Other</td>
</tr>
<tr>
<td>Health / Meditation</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Meditation</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Other</td>
</tr>
<tr>
<td>Health / Pregnancy</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Pregnancy</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Family Planning</td>
</tr>
<tr>
<td>Health / Sleep Trackers</td>
  <td>Health &amp; Fitness</td>
  <td>Health &amp; Fitness / Sleep Trackers</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Health &amp; Fitness / Other</td>
</tr>
<tr>
<td>Cooking</td>
  <td>Health &amp; Fitness</td>
  <td>Cooking</td>
  <td>Health</td>
  <td>Health</td>
  <td>Health/Fitness</td>
  <td>Home &amp; Hobby / Cooking</td>
</tr>
<tr>
<td>Utilities</td>
  <td>Libraries &amp; Demo</td>
  <td>Utilities / Other</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities</td>
</tr>
<tr>
<td>Utilities / Developer</td>
  <td>Libraries &amp; Demo</td>
  <td>Utilities / Other</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Developer – Programmer</td>
</tr>
<tr>
<td>Utilities / Other</td>
  <td>Libraries &amp; Demo</td>
  <td>Utilities / Other</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Utilities / Security</td>
  <td>Libraries &amp; Demo</td>
  <td>Utilities / Other</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Security</td>
</tr>
<tr>
<td>Alarms &amp; Clocks</td>
  <td>Tools</td>
  <td>Utilities / Alarms &amp; Clocks</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Battery Savers</td>
  <td>Tools</td>
  <td>Utilities / Battery Savers</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Calculators</td>
  <td>Tools</td>
  <td>Utilities / Calculators</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Calendars</td>
  <td>Tools</td>
  <td>Utilities / Calendars</td>
  <td>Organizers</td>
  <td>Organizers</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Notes</td>
  <td>Tools</td>
  <td>Utilities / Notes</td>
  <td>Organizers</td>
  <td>Organizers</td>
  <td>Utilities</td>
  <td>Tools &amp; Utilities / Other</td>
</tr>
<tr>
<td>Productivity</td>
  <td>Productivity</td>
  <td>Productivity</td>
  <td>Organizers</td>
  <td>Organizers</td>
  <td>Productivity</td>
  <td>Productivity</td>
</tr>
<tr>
<td>Music</td>
  <td>Music &amp; Audio</td>
  <td>Music / Other</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music</td>
</tr>
<tr>
<td>Music / Artists</td>
  <td>Music &amp; Audio</td>
  <td>Music / Artists</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music / Other</td>
</tr>
<tr>
<td>Music / Instruments</td>
  <td>Music &amp; Audio</td>
  <td>Music / Instruments</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music / Instruments</td>
</tr>
<tr>
<td>Music Players</td>
  <td>Music &amp; Audio</td>
  <td>Music / Music Players</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music / Music players</td>
</tr>
<tr>
<td>Radio</td>
  <td>Music &amp; Audio</td>
  <td>Music / Radio</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music / Radio</td>
</tr>
<tr>
<td>Music / Songbooks</td>
  <td>Music &amp; Audio</td>
  <td>Music / Songbooks</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Music/Video</td>
  <td>Music / Other</td>
</tr>
<tr>
<td>Photography</td>
  <td>Photography</td>
  <td>Photography</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Photo</td>
  <td>Photography</td>
</tr>
<tr>
<td>Photography / Camera</td>
  <td>Photography</td>
  <td>Photography</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Photo</td>
  <td>Photography / Camera</td>
</tr>
<tr>
<td>Photography / Editing</td>
  <td>Photography</td>
  <td>Photography</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Photo</td>
  <td>Photography / Editing</td>
</tr>
<tr>
<td>Photography / Gallery</td>
  <td>Photography</td>
  <td>Photography</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Photo</td>
  <td>Photography / Gallery</td>
</tr>
<tr>
<td>Photography / Sharing</td>
  <td>Photography</td>
  <td>Photography</td>
  <td>Multimedia</td>
  <td>Multimedia</td>
  <td>Photo</td>
  <td>Photography / Sharing</td>
</tr>
<tr>
<td>Personalization</td>
  <td>Personalization</td>
  <td>Themes</td>
  <td>Themes &amp; Skins</td>
  <td>Themes &amp; Skins</td>
  <td>Theme</td>
  <td>Themes</td>
</tr>
<tr>
<td>Live Wallpapers</td>
  <td>Personalization</td>
  <td>Themes</td>
  <td>Themes &amp; Skins</td>
  <td>Themes &amp; Skins</td>
  <td>Theme</td>
  <td>Themes / Live Wallpapers</td>
</tr>
<tr>
<td>Wallpapers</td>
  <td>Personalization</td>
  <td>Themes</td>
  <td>Themes &amp; Skins</td>
  <td>Themes &amp; Skins</td>
  <td>Theme</td>
  <td>Themes / Wallpapers</td>
</tr>
<tr>
<td>Ringtones</td>
  <td>Personalization</td>
  <td>Ringtones / Other</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Christian</td>
  <td>Personalization</td>
  <td>Ringtones / Christian</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Classical</td>
  <td>Personalization</td>
  <td>Ringtones / Classical</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Collegiate</td>
  <td>Personalization</td>
  <td>Ringtones / Collegiate</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Comedy</td>
  <td>Personalization</td>
  <td>Ringtones / Comedy</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Country</td>
  <td>Personalization</td>
  <td>Ringtones / Country</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Dance &amp; Electronic</td>
  <td>Personalization</td>
  <td>Ringtones / Dance &amp; Electronic</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Jazz &amp; Standards</td>
  <td>Personalization</td>
  <td>Ringtones / Jazz &amp; Standards</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Latin</td>
  <td>Personalization</td>
  <td>Ringtones / Latin</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Pop</td>
  <td>Personalization</td>
  <td>Ringtones / Pop</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Rap</td>
  <td>Personalization</td>
  <td>Ringtones / Rap</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Rock</td>
  <td>Personalization</td>
  <td>Ringtones / Rock</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Sound Effects</td>
  <td>Personalization</td>
  <td>Ringtones / Sound Effects</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Soundtracks</td>
  <td>Personalization</td>
  <td>Ringtones / Soundtracks</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Sports</td>
  <td>Personalization</td>
  <td>Ringtones / Sports</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / TV</td>
  <td>Personalization</td>
  <td>Ringtones / TV</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
<tr>
<td>Ringtones / Voicetones</td>
  <td>Personalization</td>
  <td>Ringtones / Voicetones</td>
  <td>Ringtones</td>
  <td>Ringtones</td>
  <td>Music/Video</td>
  <td>Themes / Ringtones</td>
</tr>
</table>

### Game Categories
<table>
<tr>
  <th>Category</th>
  <th>Google Play</th>
  <th>Amazon AppStore</th>
  <th>Opera Store</th>
  <th>Yandex.Store</th>
  <th>Samsung Apps</th>
  <th>SlideMe</th>
</tr>
<tr>
<td>Games / Puzzles</td>
  <td>Brain &amp; Puzzle</td>
  <td>Games / Puzzles &amp; Trivia</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Puzzle</td>
  <td>Fun &amp; Games / Puzzle</td>
</tr>
<tr>
<td>Games / Trivia</td>
  <td>Brain &amp; Puzzle</td>
  <td>Games / Puzzles &amp; Trivia</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Word/Trivia</td>
  <td>Fun &amp; Games / Other</td>
</tr>
<tr>
<td>Games / Other</td>
  <td>Casual</td>
  <td>Games / Other</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Other</td>
</tr>
<tr>
<td>Games / Drawing</td>
  <td>Casual</td>
  <td>Games / Other</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Drawing</td>
</tr>
<tr>
<td>Games / Casual</td>
  <td>Casual</td>
  <td>Games / Casual</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Casual</td>
</tr>
<tr>
<td>Games / Educational</td>
  <td>Casual</td>
  <td>Games / Educational</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Educational</td>
</tr>
<tr>
<td>Games / Kids</td>
  <td>Casual</td>
  <td>Games / Kids</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Other</td>
</tr>
<tr>
<td>Games / Multiplayer</td>
  <td>Casual</td>
  <td>Games / Multiplayer</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Others</td>
  <td>Fun &amp; Games / Multiplayer</td>
</tr>
<tr>
<td>Games / Music</td>
  <td>Casual</td>
  <td>Games / Music</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Music</td>
  <td>Fun &amp; Games / Music</td>
</tr>
<tr>
<td>Games / Arcade</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Board</td>
  <td>Games</td>
  <td>Arcade</td>
  <td>Game / Arcade</td>
  <td>Fun &amp; Games / Arcade</td>
</tr>
<tr>
<td>Games / Board</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Arcade</td>
  <td>Games / Arcade</td>
  <td>Arcade</td>
  <td>Game / Board</td>
  <td>Fun &amp; Games / Board</td>
</tr>
<tr>
<td>Games / Action</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Action</td>
  <td>Games / Action</td>
  <td>Action</td>
  <td>Game / Action</td>
  <td>Fun &amp; Games / Action</td>
</tr>
<tr>
<td>Games / Adventure</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Adventure</td>
  <td>Games / Action</td>
  <td>Action</td>
  <td>Game / Adventure</td>
  <td>Fun &amp; Games / Adventure</td>
</tr>
<tr>
<td>Games / Role Playing</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Role Playing</td>
  <td>Games / Strategy</td>
  <td>Strategy</td>
  <td>Game / Role Playing</td>
  <td>Fun &amp; Games / Role Playing</td>
</tr>
<tr>
<td>Games / Strategy</td>
  <td>Arcade &amp; Action</td>
  <td>Games / Strategy</td>
  <td>Games / Strategy</td>
  <td>Strategy</td>
  <td>Game / Strategy</td>
  <td>Fun &amp; Games / Strategy</td>
</tr>
<tr>
<td>Games / Cards</td>
  <td>Cards &amp; Casino</td>
  <td>Games / Cards</td>
  <td>Games / Cards</td>
  <td>Cards</td>
  <td>Game / Card/Casino</td>
  <td>Fun &amp; Games / Cards &amp; Casino</td>
</tr>
<tr>
<td>Games / Casino</td>
  <td>Cards &amp; Casino</td>
  <td>Games / Casino</td>
  <td>Games / Cards</td>
  <td>Cards</td>
  <td>Game / Card/Casino</td>
  <td>Fun &amp; Games / Cards &amp; Casino</td>
</tr>
<tr>
<td>Games / Racing</td>
  <td>Racing</td>
  <td>Games / Racing</td>
  <td>Games / Sports</td>
  <td>Sports</td>
  <td>Game / Sports</td>
  <td>Fun &amp; Games / Racing</td>
</tr>
<tr>
<td>Games / Sports</td>
  <td>Sports Games</td>
  <td>Games / Sports</td>
  <td>Games / Sports</td>
  <td>Sports</td>
  <td>Game / Sports</td>
  <td>Fun &amp; Games / Sports</td>
</tr>
</table>

License
-------------
This file is licensed under the Creative Commons Attribution 2.5 license:
http://creativecommons.org/licenses/by/2.5/
