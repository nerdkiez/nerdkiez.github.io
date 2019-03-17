require 'html-proofer'

task default: 'test'

task :test do
  sh 'bundle exec jekyll build'
  options = { assume_extension: true }
  HTMLProofer.check_directory('./_site', options).run
end

require 'w3c_validators'

def validator(file)
  extension = File.extname(file)
  if extension == '.html'
    W3CValidators::NuValidator.new
  elsif extension == '.css'
    W3CValidators::CSSValidator.new
  end
end

def validate(file)
  puts "Checking #{file}..."

  path = File.expand_path "./_site/#{file}", __dir__
  results = validator(file).validate_file(path)

  return puts 'Valid!' if results.errors.empty?

  results.errors.each { |err| puts err.to_s }
  exit 1
end

validate 'index.html'
validate File.join 'assets', 'css', 'style.css'
