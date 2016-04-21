# tracking-new

		$tracking_item = array();
		$tracking_itemst = get_post_meta( $order_id, '_wc_shipment_tracking_items', true );

		if ( is_array( $tracking_itemst ) ) {
			if ( $formatted ) {
				foreach( $tracking_itemst as &$item ) {
					$formatted_item = $this->get_formatted_tracking_item( $order_id, $item );
					$item = array_merge( $item, $formatted_item );
				}
			}
 		}

 
		$tracking_provider = strtolower($shipment->selected_rate->carrier);
		$tracking_item[ 'tracking_provider' ]        = wc_clean( $tracking_provider );
		$tracking_item[ 'custom_tracking_provider' ] = wc_clean( $args[ 'custom_tracking_provider' ] );
		$tracking_item[ 'custom_tracking_link' ]     = wc_clean( $args[ 'custom_tracking_link' ] );
		$tracking_item[ 'tracking_number' ]          = wc_clean( $shipment->tracking_code );
		$tracking_item[ 'date_shipped' ]             = wc_clean( $date );
 		$tracking_items = $tracking_itemst;
		$tracking_items[] = $tracking_item;
		update_post_meta( $order_id, '_wc_shipment_tracking_items', $tracking_items );
