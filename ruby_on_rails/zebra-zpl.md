# zebra-zpl
> reference: https://github.com/bbulpett/zebra-zpl

自訂label.zpl

need gem: cups-0.1.10

## system lib
```
sudo apt-get install libcups2-dev
sudo apt-get install libcupsimage2-dev
```

## usage
```
label = Zebra::Zpl::Label.new :print_density => 6, :print_speed => 3
text = Zebra::Zpl::Text.new :data => "Hello, printer!", :position => [100, 100], :font_size => Zebra::Zpl::FontSize::SIZE_2
label << text

f_label = label.persist
f_label.open

File.open("#{Rails.root}/public/otherFile", 'w') { |file|
	file.write(f_label.read)
}

f_label.close
f_label.unlink
```

### notice
```
text have print_mode, value is "N" or "R"
```
