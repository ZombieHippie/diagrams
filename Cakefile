{spawn, exec} = require 'child_process'
Rehab = require 'rehab'

option '-m', '--minify', 'minify after compilation'

buildRiff = (watch=false) ->
  from_files = (new Rehab().process './coffee')
  coffee = spawn 'cmd', ["/c", "coffee", "-j", "js/script.js", "-bc"+(if watch then "w" else "")].concat from_files
  coffee.on 'error', (err) ->
    console.log 'coffee error', err
  coffee.stdout.on 'data', (data) -> console.log data.toString().trim()
  coffee.stderr.on 'data', (data) -> console.log data.toString().trim()

task 'build', 'Build riff-designer using Rehab (--minify to minify result)',(options)->
  console.log "Building coffee-script from coffee/ to js/script.js"
  buildRiff()
  if options.minify
    exec 'java -jar "lib/compiler.jar" --js js/script.js --js_output_file js/script.js', (err, stdout, stderr) ->
      throw err if err
      console.log stdout + stderr

task 'watch', 'Watch riff-designer files and compile using Rehab', ->
  console.log "Watching coffee-script from coffee/ to js/script.js"
  buildRiff(true)