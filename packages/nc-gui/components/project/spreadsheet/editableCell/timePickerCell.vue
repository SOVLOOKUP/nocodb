<template>
  <v-menu>
    <template v-slot:activator="{on}">
      <input class="value" v-on="on" v-model="localState">
    </template>
    <div @click.stop class="d-flex flex-column justify-center">
      <v-time-picker v-on="parentListeners" v-model="localState"></v-time-picker>
      <v-btn small color="primary" @click="$emit('update')">Save</v-btn>
    </div>
  </v-menu>
</template>

<script>
export default {
  name: "time-picker-cell",
  props: {
    value: [String, Date]
  },
  mounted() {
    if (this.$el && this.$el.$el) {
      this.$el.$el.focus();
    }
  },
  computed: {
    localState: {
      get() {
        return typeof this.value === 'string' ? this.value.replace(/(\d)T(?=\d)/, '$1 ') : this.value;
      },
      set(val) {
        this.$emit('input', (new Date(val).toJSON() || '').slice(0, 10) || val);
      }
    },
    parentListeners() {
      const $listeners = {};

      if (this.$listeners.blur) {
        $listeners.blur = this.$listeners.blur;
      }
      if (this.$listeners.focus) {
        $listeners.focus = this.$listeners.focus;
      }

      if (this.$listeners.cancel) {
        $listeners.cancel = this.$listeners.cancel;
      }

      return $listeners;
    },
  }
}
</script>

<style scoped>
.value {
  width:100%;
  min-height: 20px;
}
</style>
<!--
/**
 * @copyright Copyright (c) 2021, Xgene Cloud Ltd
 *
 * @author Naveen MR <oof1lab@gmail.com>
 * @author Pranav C Balan <pranavxc@gmail.com>
 *
 * @license GNU AGPL version 3 or any later version
 *
 * This program is free software: you can redistribute it and/or modify
 * it under the terms of the GNU Affero General Public License as
 * published by the Free Software Foundation, either version 3 of the
 * License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU Affero General Public License for more details.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 *
 */
-->
