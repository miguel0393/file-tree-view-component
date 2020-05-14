<template>
  <div id="app">
    <div class="content">
      <section>
          {{content}}
        <!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris placerat quis urna ut elementum. Pellentesque mattis, lectus sit amet molestie auctor, elit enim rutrum enim, ac ullamcorper metus arcu nec ex. Donec at massa lectus. Aenean ornare facilisis bibendum. Etiam laoreet metus ut mi elementum, nec convallis augue lacinia. Donec a ultricies turpis. Pellentesque porta nisi sem, nec commodo justo tincidunt et.
        In ut eros sit amet ligula cursus feugiat vitae eu velit. Nullam ac ipsum mollis, porttitor massa sit amet, interdum dui. Duis vel arcu id quam ultricies auctor. Maecenas feugiat ipsum nec quam tincidunt, et pellentesque elit bibendum. Nullam ornare augue id tristique molestie. Pellentesque rhoncus, erat sed ullamcorper consectetur, risus est fringilla risus, vel vulputate dolor tellus sit amet dolor. Aenean tristique sit amet dolor eget malesuada. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec egestas mauris eget urna pretium, quis accumsan neque scelerisque.
        Proin porta tempor aliquam. Vivamus massa enim, maximus eget congue id, euismod quis sapien. Curabitur in rutrum leo. Vestibulum feugiat mauris eu metus viverra, non ultricies nibh vestibulum. Praesent sit amet egestas erat. Curabitur aliquet dolor ut tellus semper pretium. Nullam non ipsum ac lorem commodo semper. Interdum et malesuada fames ac ante ipsum primis in faucibus.
        Phasellus congue pharetra fringilla. Aliquam pulvinar venenatis blandit. Nulla eget vehicula risus, ut consequat sapien. Nam odio felis, rhoncus ut ante non, feugiat dapibus felis. Donec at risus leo. Nullam in elementum nulla, ut placerat arcu. Donec tempus est risus, at blandit nisl eleifend quis. Aliquam a diam et augue facilisis suscipit eu quis tellus. Donec in lacinia augue. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Fusce porta lobortis leo vel dapibus.
        Sed non eros at turpis pretium bibendum non eget sem. Phasellus rutrum dui sed elit semper ullamcorper in et tellus. Quisque erat mauris, vestibulum eget nisi eu, iaculis pulvinar magna. Nulla vehicula posuere diam at ultricies. Sed eget magna iaculis, fermentum lectus a, fringilla augue. Donec iaculis in elit non bibendum. Phasellus nibh velit, tristique tincidunt leo in, luctus tempor enim. Donec malesuada interdum elit vel accumsan. -->
      </section>
    </div>
  </div>
</template>

<script>
export default {
    name: "FileContent",
    props: {
        content: String
    },
};
</script>

<style scoped>
#app {
  background-color: #34495e;
  display: inline-block;
  width: 74%;
  height: 100%;
  margin-left: 23%;
  margin-right: 3%;
}

.content {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 18px;
  text-align: left;
  margin: 20px;

}
</style>