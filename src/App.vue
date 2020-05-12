<template>
    <div class="container">
        <div class="row">
            <div class="col-12 text-center py-5">
                <h1>Download-Link Generator</h1>
            </div>
        </div>
        <div class="row">
            <div class="col-md-4">
                <div class="card p-3 shadow-sm">
                    <div class="form-group">
                        <label>Title</label>
                        <input class="form-control" type="text" id="id_title" v-model="title">
                    </div>

                    <div class="form-group">
                        <label>Description</label>
                        <input class="form-control" type="text" id="id_description" v-model="description">
                    </div>

                    <div class="form-group">
                        <label>Link</label>
                        <input class="form-control" type="text" id="id_link" v-model="link">
                    </div>

                    <div class="form-check">
                        <input class="form-check-input"
                               type="checkbox"
                               value="internal_link"
                               id="defaultCheck1"
                               v-model="checked">
                        <label class="form-check-label" for="defaultCheck1">
                            Internal Link
                        </label>
                    </div>

                    <div class="form-group">
                        <button class="btn btn-primary mr-1" v-on:click="addName">Add Link</button>
                        <button class="btn btn-secondary" v-clipboard:copy="paragraph">Copy Text</button>
                    </div>
                </div>

            </div>
            <div class="col-md-8">
                <div class="card shadow-sm p-3 mb-3">
                    <label>HTML Result</label>
                    <hr/>
                    <pre id="code">&lt;table class="table table-valign-middle table-sm table-hover"&gt;
	&lt;tbody&gt;
                        <hr/>
{{paragraph}}
                        <hr/>
	&lt;/tbody&gt;
&lt;/table&gt;</pre>
                </div>

                <div class="alert alert-info">
                    Each link goes between &lt;tr&gt; or 'table row' tags, while all links go between one &lt;table&gt; and &lt;body&gt; tag. (should this helptext be moved to the top so that it's always visible when undergrads scroll back up to copy-paste?
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    name   : 'App',
    mounted() {
      // var myCodeMirror = CodeMirror(document.getElementById('code'));
    },
    methods: {
      addName() {
        if (this.checked == true) {
          this.paragraph += '\n\t\t<tr class="no-border">\n' +
            '\t\t<td class="text-muted download-td"><i class="fa fa-file-text-o"></i></td>\n' +
            '\t\t<th>\n' +
            '\t\t\t' + this.title + '\n' +
            '\t\t\t<div>\n' +
            '\t\t\t\t<a class="text-sm text-muted font-normal" href="/' + this.link + '">' + this.description + '</a>\n' +
            '\t\t\t</div>\n' +
            '\t\t</th>\n' +
            '\t\t<td class="text-right"><a href="/' + this.link + '" class="btn btn-primary"><i class="fa fa-download"></i></a></td>\n' +
            '\t\t</tr>\n'
        } else {
          this.paragraph += '\n\t\t<tr class="no-border">\n' +
            '\t\t<td class="text-muted download-td"><i class="fa fa-file-text-o"></i></td>\n' +
            '\t\t<th>\n' +
            '\t\t\t<a href="' + this.link + '">' + this.title + '</a>\n' +
            '\t\t\t<div>\n' +
            '\t\t\t\t<a class="text-sm text-muted font-normal" href="' + this.link + '">' + this.description + '</a>\n' +
            '\t\t\t</div>\n' +
            '\t\t</th>\n' +
            '\t\t<td class="text-right"><a href="' + this.link + '" class="btn btn-primary"><i class="fa fa-download"></i></a></td>\n' +
            '\t\t</tr>\n'
        }
      },
    },
    data() {
      return {
        title      : '',
        description: '',
        link       : '',
        paragraph  : '',
        checked    : '',
      }
    },
  }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
