Add action on pushing button on handset. It changes track to next now.
This is patch to dvalik code and Android.xml files.
You must use this steps to appy patch:

$ apktool d de.illogical.modo.tablet-1.apk
$ cd de.illogical.modo.tablet-1
$ patch -p1 < de.illogical.modo.tablet-1.diff
$ cd ..
$ apktool b de.illogical.modo.tablet-1
$ cp de.illogical.modo.tablet-1/dist/de.illogical.modo.tablet-1.apk de.illogical.modo.tablet-2.apk

Now you have patched unsigned apk
To sign it you might do this steps:

Generate key (once):

$ openssl genrsa -out key.pem 1024
$ openssl req -new -key key.pem -out request.pem
$ openssl x509 -req -days 9999 -in request.pem -signkey key.pem -out certificate.pem
$ openssl pkcs8 -topk8 -outform DER -in key.pem -inform PEM -out key.pk8 -nocrypt

Sign:

$ java -jar <path>/signapk.jar certificate.pem key.pk8 de.illogical.modo.tablet-2.apk de.illogical.modo.tablet-3.apk

Now you can install or send it to you friends

$ adb install de.illogical.modo.tablet-3.apk
