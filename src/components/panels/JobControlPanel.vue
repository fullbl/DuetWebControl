<template>
	<v-card>
		<v-card-title class="pb-1">
			<v-icon small class="mr-1">mdi-wrench</v-icon> {{ $t('panel.jobControl.caption') }}
		</v-card-title>

		<v-card-text class="pt-0">
			<job-btns></job-btns>

			<v-menu v-if="thumbnails.some(thumbnail => thumbnail.data !== null)" open-on-click offset-y>
				<template #activator="{ attrs, on }">
					<v-btn color="info" block :disabled="uiFrozen" class="mt-3" v-bind="attrs" v-on="on">
						<v-icon class="mr-1">mdi-image</v-icon> {{ $t('panel.jobControl.showPreview' )}}
					</v-btn>
				</template>

				<v-card>
					<v-carousel height="auto" hide-delimiters :show-arrows="validThumbnails.length > 1" show-arrows-on-hover>
						<v-carousel-item v-for="thumbnail in validThumbnails" :key="`${thumbnail.format}-${thumbnail.width}x${thumbnail.height}`">
							<div class="d-flex fill-height align-center">
								<thumbnail-img :thumbnail="thumbnail" class="mx-auto"/>
							</div>
						</v-carousel-item>
					</v-carousel>
				</v-card>
			</v-menu>
		</v-card-text>
	</v-card>
</template>

<script>
'use strict'

import { mapState, mapGetters } from 'vuex'

import JobBtns from '../buttons/JobBtns.vue'

export default {
	components: { JobBtns },
	computed: {
		...mapState('machine/model', {
			thumbnails: state => state.job.file.thumbnails
		}),
		...mapGetters(['uiFrozen']),
		validThumbnails() {
			return this.thumbnails.filter(thumbnail => !!thumbnail.data);
		}
	}
}
</script>
