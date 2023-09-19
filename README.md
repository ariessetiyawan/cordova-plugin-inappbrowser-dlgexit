# cordova-plugin-inappbrowser-dlgexit
 Add dialog exit in plugin inappbrowser event exit

To display external website URLs in Cordova, you can use the inappbrowser plugin. For integration with backbuttons and exit dialogs.

![at3cNiWGKE](https://github.com/ariessetiyawan/cordova-plugin-inappbrowser-dlgexit/assets/99067179/9a96b29e-68b7-4247-aac8-d1736b51cab6)

InAppBrowserDialog.java

```
.....
public void onBackPressed () {
        if (this.inAppBrowser == null) {
            this.dismiss();
        } else {
            if (this.inAppBrowser.hardwareBack() && this.inAppBrowser.canGoBack()) {
                this.inAppBrowser.goBack();
            }  else {
                //this.inAppBrowser.closeDialog();
				AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(context)
				.setTitle("Exit")
				.setMessage("You are about to exit, are you sure?")
				.setPositiveButton("Exit", new DialogInterface.OnClickListener(){
					public void onClick(DialogInterface dialog, int which){
						if (inAppBrowser == null) {
							dismiss();
						} 
						else {
							// better to go through the in inAppBrowser
							// because it does a clean up
							if (inAppBrowser.hardwareBack() && inAppBrowser.canGoBack()) {
								inAppBrowser.goBack();
							}  else {
								inAppBrowser.closeDialog();
							}
						}
					}
				})
				.setNegativeButton("Cancel", new DialogInterface.OnClickListener(){
					public void onClick(DialogInterface dialog,int which){
						dialog.cancel();
					}
				});
				alertDialogBuilder.create();
				alertDialogBuilder.show();
            }
        }
    }
```
