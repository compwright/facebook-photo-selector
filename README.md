# Facebook Photo Selector

An easy-to-use Facebook Photo Selector jQuery plugin built for Twitter Bootstrap.

[View Demo]() or [Download the Plugin]()

## License

This work is published under the [MIT License](http://opensource.org/licenses/MIT).

## Usage

### Initializing the Facebook SDK

This plugin needs a fully-working instance of the [Facebook Javascript SDK](), which you can set by calling `FacebookPhotoSelector.setFacebookSDK()`.

```
$.getScript('//connect.facebook.net/en_US/all.js', function()
{
	FB.init({
		appId      : 'YOUR-APP-ID',
		channelUrl : '//your-domain.com/fb-channel.html',
		status     : true,
		xfbml      : false
	});

	FacebookPhotoSelector.setFacebookSDK(FB);
});
```

### Photo Selector Modal

Set up a Twitter Bootstrap modal similar to the following:

```
<!-- Facebook photo selector modal -->
<div id="facebook_photo_selector" class="modal fade">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
				<h4 class="modal-title">Choose a photo</h4>
			</div>
			<div class="modal-body">
				<div class="form">
					<label>Select Facebook Album:</label>
					<select class="fbps-albums" name="facebook_photo_album"></select>
				</div>
				<hr>
				<div class="fbps-photos clearfix"></div>
			</div>
			<div class="modal-footer">
				<button type="button" class="btn btn-default fbps-cancel" data-dismiss="modal">Close</button>
				<button type="button" class="btn btn-primary fbps-select" data-dismiss="modal">Select Photo</button>
			</div>
		</div><!-- /.modal-content -->
	</div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```

Note that you do not have to follow this exact markup. All of the CSS classes may be customized.

The following CSS is also recommended so that the scrolling, loading indicator, and selected states work properly.

```
<style type="text/css">
	.thumbnail.selected {
		background-color: #428bca;
	}
	.loading {
		text-align: center;
	}
	.modal-body {
		max-height: 600px;
		overflow-y: auto;
	}
</style>
```

### Activate the jQuery Plugin

To use the plugins, simply call the `.facebookPhotoSelector()` plugin on your modal.

```
$('#facebook_photo_selector').facebookPhotoSelector({
	onFinalSelect : function(photos)
	{
		console.log(photos);
	}
});
```

## Configuration

Global defaults may be set using `$.fn.facebookPhotoSelector.defaults` or they may be passed when you activate the plugin.

Here is a full list of available options:

```
$.fn.facebookPhotoSelector.defaults = {
	fbsdkPollInterval : 100,              // Polling interval in milliseconds to use when waiting for the Facebook SDK
	selectors : {
		albums    : 'select.fbps-albums', // selector for the album list container
		photos    : '.fbps-photos',       // selector for the photo list container
		btnCancel : '.fbps-cancel',       // selector for the "Cancel" button
		btnSelect : '.fbps-select'        // selector for the "Select Photo" button
	},
	fbsdk         : false,                // Facebook Javascript SDK instance
	fbscope       : 'user_photos',        // CSV list of Facebook permissions required
	photoColumns  : 4,                    // Number of columns to display photos in
	photosPerPage : 20,                   // Number of photos to load at a time
	selectLimit   : 1,                    // Number of photos that may be selected at a time
	onBeforeInit  : function() {},
	onLoadPhotos  : function() {},
	onLoadAlbums  : function() {},
	onAlbumChange : function() {},
	onSelect      : function() {},
	onFinalSelect : function() {}
};
```

## Callbacks

Callback                        | Description
--------------------------------|--------------------------------------------------------------------------------------
onBeforeInit(modal)             | Fires before the plugin initializes a modal. Will be called once per modal.
onLoadPhotos(container, photos) | Fires whenever photos are loaded from Facebook.
onLoadAlbums(container, albums) | Fires whenever albums are loaded from Facebook.
onAlbumChange(albumId)          | Fires when the user changes photo albums.
onSelect(photoId)               | Fires when the user selects a photo.
onFinalSelect(photos)           | Fires when the user clicks Select Photo button as specified by `selectors.btnSelect`.

