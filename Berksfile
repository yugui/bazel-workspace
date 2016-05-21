source 'https://supermarket.getchef.com'

Dir['cookbooks/*'].each do |path|
  metadata path: path if File.directory?(path)
end

cookbook 'java'
