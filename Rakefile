require "erb"
require "yaml"

class Artifact
  attr_reader :id

  def initialize(filename)
    @id = File.basename(filename, ".yaml")
    @data = YAML.load_file(filename)
  end

  def name
    @data["name"]
  end

  def filename
    @data["filename"]
  end

  def depends
    @data["depends"] || []
  end

  def require
    @data["require"] || []
  end

  def url
    @data["url"]
  end

  def node
    ERB.new(File.read("./templates/node.dot.erb"), trim_mode: "-").result(binding)
  end

  def edges
    ERB.new(File.read("./templates/edges.dot.erb"), trim_mode: "-").result(binding)
  end
end

file "voxoculi.svg" => "voxoculi.dot" do |t|
  sh "dot -Tsvg -o #{t.name} #{t.prerequisites.join(" ")}"
end

file "voxoculi.dot" => Dir["*.yaml", "templates/*.dot.erb"] do |t|
  puts "GEN #{t.name}"
  @artifacts = Dir["*.yaml"].map { |yaml| Artifact.new(yaml) }

  File.write(t.name, ERB.new(File.read("./templates/graph.dot.erb"), trim_mode: "-").result(binding))
end

desc "Check syntax"
task "lint" do
  sh "check-jsonschema --schemafile schema/schema.yaml *.yaml"
end

task default: "voxoculi.svg"
