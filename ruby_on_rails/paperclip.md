# Paperclip
> references: https://github.com/thoughtbot/paperclip

> http://www.rubydoc.info/gems/paperclip/Paperclip

圖片上傳

需要用到imagemagick

## depend
```
imagemagick: https://github.com/ImageMagick/ImageMagick
ubuntu lib: sudo apt-get install imagemagick
```

## migration
```
class CreateUsersWithAttachments < ActiveRecord::Migration
	def change
		create_table :users do |t|
			t.attachment :avatar
		end
	end
end

class AddAttachmentColumnsToUsers < ActiveRecord::Migration
	def change
		add_attachment :users, :avatar
	end
end
```

## model
```
class User < ActiveRecord::Base
	has_attached_file :avatar, styles: lambda { |attachment| { thumb: (attachment.instance.boss? ? "300x300>" : "100x100>") } }
	has_attached_file :image1, default_url: "/default_image.svg", styles: { thumb: "100x100>", email: "600x600>", pdf: "300x300>" }
end
```
