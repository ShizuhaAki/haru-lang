# Harulang
This repository holds the specification for Harulang, the scripting language used by haru, a galgame engine currently in development.

Despite the name *scripting language*, Harulang is actually XML designed to be both machine- and human- readable.

## A Minimum Example
```xml
<haru>
  <project>
    <resource-dir> "./resources" </resource-dir>
  </project>
  <character name="Reimu" img="/reimu">r</character>
  <character name="Marisa" img="/Marisa">m</character>
  <variable value="6" type="int">san</variable>
  <scene id="main">
    <background>default.png</background>
    <show at="left">r</show>
    <show at="right">m</show>
    <line from="r" sprite="happy">
      This is a line spoken by character Reimu
    </line>
    <line from="m" sprite="normal">
      This is another line spoken by Marisa
    </line>
    <select>
      <choice prompt="First choice">
        <expr>san := san - 1</expr>
      </choice>
      <choice prompt="Second choice">
        <expr>san := san - 2 </expr>
      </choice>
    </select>
    <if condition="san > 5">
      <then>
        <jump target="high-san"/>
      </then>
      <else>
        <jump target="low-san">
      </else>
    </if>
  </scene>
</haru>
```