<template>
	<v-row :dense="$vuetify.breakpoint.mobile">
		<v-col cols="12" sm="6" md="4" lg="4" xl="4">
			<status-panel></status-panel>
		</v-col>

		<v-col cols="12" sm="6" md="5" lg="5" xl="4">
		</v-col>
	</v-row>
</template>

<script>
'use strict'

import { mapGetters } from 'vuex'

export default {
	computed: {
		...mapGetters('machine', ['hasTemperaturesToDisplay'])
	}
}
</script>