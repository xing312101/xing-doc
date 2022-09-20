# Zip File with mutiple file
> shopify 上傳csv資料有上限，所以需要切割資料，以10000筆做分割，然後下載成一個ZIP，再手動將csv一個一個丟進shopify

```
require 'csv'
users = User.select([:first_name, :last_name, :email, :address1, :address2, :city, :state, :country, :zip, :phone]);
slice_users = users.each_slice(10000).to_a;
tmp_file = Tempfile.new("user_temp.zip");
::Zip::OutputStream.open(tmp_file){|zos|};
::Zip::File.open(tmp_file, Zip::File::CREATE) do |zip|
	slice_users.each_with_index do |partial_users, index|
		csv_file = CSV.generate() do |csv|
			csv << ['First Name', 'Last Name', 'Email', 'Address1', 'Address2', 'City', 'Province Code', 'Country', 'Zip', 'Phone'];
				partial_users.each do |user|
					csv << [user.first_name, user.last_name, user.email, user.address1, user.address2, user.city, user.state, user.country, user.zip, user.phone];
				end
			end
		zip.get_output_stream("users_#{index}.csv") { |f| f.puts(csv_file) }
	end
end
file_name = "users-for-shopify-#{Time.now.to_i}.zip"
zip_data = File.read(tmp_file.path)
send_data(zip_data, type: 'application/zip', filename: file_name)
```
