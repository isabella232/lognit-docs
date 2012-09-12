require 'ejs'

guard 'compass', :configuration_file => './compass.rb' do
  watch(/^(.*)\.s[ac]ss/)
end

guard 'livereload' do
  watch(%r{^public/assets/.*\.css$})
end

asset_paths = %w(javascripts/app javascripts/vendor templates)

guard 'sprockets', :destination => "public/assets", :asset_paths => asset_paths do
  watch (%r{javascripts/vendor/.*\.js$}) {"dependencies.js"}
  watch (%r{javascripts/app/.*\.js$}) {"application.js"}
  watch (%r{templates/.*\.ejs}) {"application.js"}
end
