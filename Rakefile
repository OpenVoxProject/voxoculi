# frozen_string_literal: true

require 'voxpupuli/rubocop/rake'

file 'voxoculi.svg' => 'voxoculi.dot' do |t|
  sh "dot -Tsvg -o #{t.name} #{t.prerequisites.join(' ')}"
end

file 'voxoculi.dot' => Dir['*.yaml', 'templates/*.dot.erb'] do |t|
  sh "exe/filter --output=#{t.name}"
end

desc 'Check syntax'
task 'lint' do
  require 'json-schema'

  error = false
  schema = YAML.load_file('schema/schema.yaml')
  Dir['*.yaml'].each do |yaml|
    JSON::Validator.validate!(schema, YAML.load_file(yaml))
  rescue JSON::Schema::ValidationError => e
    warn("#{yaml}: #{e.class.name}: #{e.message}")
    error = true
  end

  abort('Validation failed') if error
end

task default: 'voxoculi.svg'
