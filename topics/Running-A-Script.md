# Running A Script

Lets say you've spun up a ruby:3.3 container and want to run a script on it. For simplicity, let's assume you have this script:
<code-block lang="ruby">
Bin = Struct.new(:bin, :quantity)

requests = [
    Bin.new(001, 1)
]

Label = Struct.new(:barcode) do
    def zpl
        <<~STR 
            ^XA^BY8,2,180^FO120,20^BC^FDB-#{sprintf("%04d", barcode)}^FS^XZ
        STR
    end
end

zpl = []

for req in requests
    req.quantity.times do |i|
        label = Label.new(req.bin + i)
        2.times {
            zpl << label.zpl
        }
        end
    end
end
</code-block>
If you copy and paste this into your console, it will run as expected. In this example, it is taking a request for a bin barcode,
plumbing the correct information into the relevant zpl, and putting the resulting string into the <code>zpl</code> array. You can test that this worked
by using <code>puts zpl</code> and should get:
<code-block lang="ruby">
"^XA^BY8,2,180^FO120,20^BC^FDB-0001^FS^XZ"
</code-block>

There's lots more you can do with containers, docker images, k8s clusters, scripts, etc etc etc - but this will give you
a reference point for remembering how to run scripts that I give you to test.
<warning>Remember: This container only exists in its own context. If you try to call anything not defined by what you
enter, it will fail - the obvious example being that <code>Resque.enqueue</code> will not work in this environment.</warning>